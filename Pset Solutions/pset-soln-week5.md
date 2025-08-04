HOMEWORK:

2.7

(define (upper-bound interval)
  (cdr interval))

(define (lower-bound interval)
  (car interval))

2.8

;; The smallest possible value for A-B is (smallest A)-(largest B).
;; Likewise, the largest value is (largest A)-(smallest B).

(define (sub-interval x y)
  (add-interval x (make-interval (- (upper-bound y))
				 (- (lower-bound y)))))

;; It would also be okay to replicate the structure of add-interval instead of
;; using add-interval as a subprocedure, although this isn't exactly following
;; Alyssa's method as the problem suggests:

(define (sub-interval x y)
  (make-interval (- (lower-bound x) (upper-bound y))
		 (- (upper-bound x) (lower-bound y)) ))


2.10

;; An interval spans zero if its lower bound is negative (or zero) and
;; its upper bound is positive (or zero).
;; It's only the divisor that we have to worry about.

(define (div-interval x y)
  (if (and (<= (lower-bound y) 0)
	   (>= (upper-bound y) 0))
      (error "Can't divide by an interval that spans zero.")
      (mul-interval x
		    (make-interval (/ 1 (upper-bound y))
				   (/ 1 (lower-bound y))))))



2.12

(define (make-center-percent c p)
  (let ((w (* c p 0.01)))
    (make-interval (- c w) (+ c w))))

;; We multiply by 0.01 because p percent is a factor of p/100.
;; If you forgot about that part, it's a relatively minor error
;; for computer science purposes, although rather serious in a
;; practical engineering situation!

(define (percent i)
  (* 100 (/ (/ (- (upper-bound i) (lower-bound i)) 2)
	    (/ (+ (lower-bound i) (upper-bound i)) 2))))

;; Slightly more efficient percent:

(define (percent i)
  (* 100 (/ (- (upper-bound i) (lower-bound i))
	    (+ (lower-bound i) (upper-bound i)))))

;; Alternate versions, using the center-width procedures we already have:

(define (make-center-percent c p)
  (make-center-width c (* c p 0.01)))

(define (percent i)
  (* 100 (/ (width i) (center i))))


2.17

(define (last-pair lst)
  (if (null? (cdr lst))
      lst
      (last-pair (cdr lst))))


2.20

The difficulty in writing recursive procedures that take any number of
arguments is that you're going to be tempted to make a recursive call
with only one argument, namely a list containing some of the original
arguments, sort of like this:

(define (same-parity . numbers)
  (cond ((null? (cdr numbers)) numbers)
	((equal? (even? (car numbers))
		 (even? (cadr numbers)))
	 (cons (car numbers)
	       (same-parity (cdr numbers))))   ; WRONG!
	(else (same-parity (cons (car numbers) (cddr numbers))))))   ; WRONG!

(define (even? num)
  (= (remainder num 2) 0))

Instead, the easiest thing to do is to define a helper procedure that
*does* expect a list of numbers as its one argument.  An advantage is
that we can then separate out the first number, which is always
accepted, as a special case:

(define (same-parity tester . others)
  (define (helper numlist)
    (cond ((null? numlist) nil)
	  ((equal? (even? tester) (even? (car numlist)))
	   (cons (car numlist) (helper (cdr numlist))))
	  (else (helper (cdr numlist)))))
  (cons tester (helper others)))

Once we know about higher-order functions, there's an even easier
solution:

(define (same-parity tester . others)
  (cons tester
	(filter (lambda (num) (equal? (even? tester) (even? num)))
		others)))


2.22.  What's wrong with iterative square-list?

I've sort of answered this already, in talking about 2.18 (iterative
reverse).  A list (as opposed to an arbitrary list structure) MUST be made
with

(cons new-member rest-of-list)

and not the other way around.  That's why Louis's second try fails; he's
making something that isn't a list, even though he does have the members
in correct left-to-right order.  He gets

((((() . 1) . 4) . 9) . 16)

instead of (1 4 9 16), which in dotted representation would be

(1 . (4 . (9 . (16 . ()))))

Louis's first try fails because he starts by consing the square of 1 onto
the empty list, etc.

Here's an iterative square-list:

(define (square-list x)
  (define (iter list answer)
    (if (null? list)
	answer
	(iter (cdr list)
	      (cons (square (car list))
		    answer))))
  (reverse (iter x nil)))

In this version, iter is O(n) time and O(1) space, as desired.  If we
use the iterative definition of reverse, it too is O(n) time and O(1) space.
So the whole thing is reasonably efficient in both time and space, even
though it has what seems to be a redundant pass through the list to reverse
it.  If you're dealing with very large lists on very small computers, this
is sometimes the only way to get an answer at all.


2.23

(define (for-each proc lst)
  (if (null? lst)
      #t
      (let ((ignored-result (proc (car lst))))
	(for-each proc (cdr lst)))))

Several people said, "Why not just use map?"  There are two answers.
First, it's inefficient because map will construct a list of all the
results, and we don't care about the results.  Second, map does not
guarantee to apply the procedure argument to the list elements in
left-to-right order.

If you think it's inelegant to have a variable ignored-result whose
value is something we don't care about, you're right.  In chapter 3
we'll learn about an alternative notation:

(define (for-each proc lst)
  (if (null? lst)
      #t
      (begin (proc (car lst))
	     (for-each proc (cdr lst)))))

And it turns out that a COND clause can contain more than two expressions,
so this can also be written as

(define (for-each proc lst)
  (cond ((null? lst) #t)
	(else (proc (car lst))
	      (for-each proc (cdr lst)))))



SUBSTITUTE:

For reference, here's the SUBSTITUTE for sentences from week 2 lab:

(define (substitute sent old new)
  (cond ((empty? sent) '())
	((equal? (first sent) old)
	 (se new (substitute (butfirst sent) old new)))
	(else (se (first sent) (substitute (butfirst sent) old new)))))

If we just change the sentence constructor/selector functions to the proper
ones for lists, and one formal parameter's name, we get this:

(define (substitute LST old new)	;; first try
  (cond ((NULL? LST) '())
	((equal? (CAR LST) old)
	 (CONS new (substitute (CDR LST) old new)))
	(else (CONS (CAR LST) (substitute (CDR LST) old new)))))

Why CONS rather than LIST or APPEND?  Because we're combining some function of
the CAR of a pair with some function (namely a recursive call) of the CDR,
trying to build a new structure with the same shape as the original.  LIST or
APPEND would change the shape; if we used LIST, all the lists we made would
have exactly two elements, but if we used APPEND, we would be flattening
sublists into, essentially, a sentence.

But this isn't good enough, because it doesn't examine sublists.  The most
obvious solution would be to add a clause to the COND to distinguish sublists
from atomic (non-list) elements:

(define (substitute lst old new)
  (cond ((null? lst) '())
	((equal? (car lst) old)
	 (cons new (substitute (cdr lst) old new)))
	((PAIR? (CAR LST))
	 (CONS (SUBSTITUTE (CAR LST) OLD NEW)
	       (SUBSTITUTE (CDR LST) OLD NEW)))
	(else (cons (car lst) (substitute (cdr lst) old new)))))

This works.  But once we're familiar with the idioms of tree recursion
(week 6), we can see a slightly more elegant solution:

(define (substitute lst old new)
  (cond ((null? lst) '())
	((equal? LST old) NEW)
	((pair? LST)
	 (cons (substitute (car lst) old new)
	       (substitute (cdr lst) old new)))
	(else LST)))

The ELSE clause is reached when the LST argument is a word rather than
a list, and is not equal to OLD.  (A list is either null or a pair.)



SUBSTITUTE2:

This will have the same program structure as SUBSTITUTE, but the EQUAL? test
is replaced by something a little more complicated.

The straightforward solution is to use MEMBER in place of EQUAL?, and then, if
a true answer is returned, look for the right thing to substitute:

(define (substitute2 lst olds news)
  (cond ((null? lst) '())
	((MEMBER lst olds)
	 (FIND-MATCH LST OLDS NEWS))
	((pair? lst)
	 (cons (substitute2 (car lst) olds news)
	       (substitute2 (cdr lst) olds news)))
	(else lst)))

(define (find-match element olds news)
  (cond ((null? olds) #f)	; This shouldn't happen
	((equal? element (car olds))
	 (car news))
	(else (find-match element (cdr olds) (cdr news)))))

This works fine.  But it's a little inelegant that we end up looking for the
element in OLDS twice, once with MEMBER and once again with FIND-MATCH.  We
can photograph two birds with one stone if we replace the first COND clause
of find-match with one that returns the value we actually want if ELEMENT
isn't found in OLDS:

(define (substitute2 lst olds news)
  (cond ((null? lst) '())
	((pair? lst)
	 (cons (substitute2 (car lst) olds news)
	       (substitute2 (cdr lst) olds news)))
	(else (FIND-MATCH LST OLDS NEWS))))

(define (find-match element olds news)
  (cond ((null? olds) ELEMENT)
	((equal? element (car olds))
	 (car news))
	(else (find-match element (cdr olds) (cdr news)))))

This version of SUBSTITUTE2 has one fewer COND clause.  The two clauses
for lists remain, and the ELSE clause now handles all words, whether or
not they're members of OLDS.



Extra for experts:

(define (cxr-function name)
  (define (helper name)
    (if (empty? name)
	(lambda (x) x)
	(compose (if (equal? (first name) 'a) car cdr)
		 (helper (bf name)))))
  (helper (bf (bl name))))	; eliminate C and R from name

(define (compose f g)
  (lambda (x) (f (g x))))

If you didn't think to use COMPOSE, you could of course do the same thing
without it, a little less neatly:

(define (cxr-function name)
  (define (helper name)
    (if (empty? name)
	(lambda (x) x)
	(lambda (x) ((if (equal? (first name) 'a) car cdr)
		     ((helper (bf name)) x)))))
  (helper (bf (bl name))))	; eliminate C and R from name