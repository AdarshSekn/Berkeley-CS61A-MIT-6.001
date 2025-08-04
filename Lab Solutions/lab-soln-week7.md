LAB ASSIGNMENT:

2.62.  Union-set in Theta(n) time.

The key is to realize the differences between union-set and
intersection-set.  The null case for union-set will be different, because if
one of the sets is empty, the result must be the other set. In the element
comparisons, one element will always be added to the result set.  So the
expressions with the element will be the same as intersection-set, only with
a cons added.  Here's the solution:

(define (union-set set1 set2)
   (cond ((null? set1) set2)
         ((null? set2) set1)
         (else (let ((x1 (car set1)) (x2 (car set2)))
                    (cond ((= x1 x2)
                           (cons x1 (union-set (cdr set1) (cdr set2))))
                          ((< x1 x2)
                           (cons x1 (union-set (cdr set1) set2)))
                          ((< x2 x1)
                           (cons x2 (union-set set1 (cdr set2)))))))))


Trees on page 156:

(define tree1
  (adjoin-set 1
   (adjoin-set 5
    (adjoin-set 11
     (adjoin-set 3
      (adjoin-set 9
       (adjoin-set 7 '())))))))

(define tree2
  (adjoin-set 11
   (adjoin-set 5
    (adjoin-set 9
     (adjoin-set 1
      (adjoin-set 7
       (adjoin-set 3 '())))))))

(define tree3
  (adjoin-set 1
   (adjoin-set 7
    (adjoin-set 11
     (adjoin-set 3
      (adjoin-set 9
       (adjoin-set 5 '())))))))

Other orders are possible; the constraint is that each node must be
added before any node below it.  So in each case we first adjoin the
root node, then adjoin the children of the root, etc.  To make sure
this is clear, here's an alternative way to create tree1:

(define tree1
  (adjoin-set 11
   (adjoin-set 9
    (adjoin-set 5
     (adjoin-set 1
      (adjoin-set 3
       (adjoin-set 7 '())))))))


2.74 (Insatiable Enterprises):

(a)  Each division will have a private get-record operation, so each
division's package will look like this:

(define (install-research-division)
  ...
  (define (get-record employee file)
    ...)
  ...
  (put 'get-record 'research get-record)
  ...)

Then we can write a global get-record procedure like this:

(define (get-record employee division-file)
  ((get 'get-record (type-tag division-file))
   employee
   (contents division-file)))

It'll be invoked, for example, like this:
            (get-record '(Alan Perlis) research-personnel-list)

For this to work, each division's file must include a type tag
specifying which division it is.

If, for example, a particular division file is a sequence of
records, one per employee, and if the employee name is the CAR of 
each record, then that division can use ASSOC as its get-record
procedure, by saying

  (put 'get-record 'manufacturing assoc)

in its package-installation procedure.


(b)  The salary field might be in a different place in each
division's files, so we have to use the right selector based
on the division tag.

(define (get-salary record)
  (apply-generic 'salary record))

Each division's package must include a salary selector, comparable
to the magnitude selectors in the complex number example.

Why did I use GET directly in (a) but apply-generic in (b)?  In the
case of get-salary, the argument is a type-tagged datum.  But in the
case of get-record, there are two arguments, only one of which (the
division file) has a type tag.  The employee name, I'm assuming,
is not tagged.


(c)  Find an employee in any division

(define (find-employee-record employee divisions)
  (cond ((null? divisions) (error "No such employee"))
	((get-record employee (car divisions)))
	(else (find-employee-record employee (cdr divisions)))))

This uses the feature that a cond clause with only one expression
returns the value of that expression if it's not false.


(d)  To add a new division, you must create a package for the division,
make sure the division's personnel file is tagged with the division name,
and add the division's file to the list of files used as argument to
find-employee-record.


4.  Scheme-1 stuff.

(a)  ((lambda (x) (+ x 3)) 5)

Here's how Scheme-1 handles procedure calls (this is a COND clause
inside EVAL-1):

       ((pair? exp) (apply-1 (eval-1 (car exp))      ; eval the operator
                             (map eval-1 (cdr exp)))); eval the args

The expression we're given is a procedure call, in which the procedure
(lambda (x) (+ x 3)) is called with the argument 5.

So the COND clause ends up, in effect, doing this:

	(apply-1 (eval-1 '(lambda (x) (+ x 3))) (map eval-1 '(5)))

Both lambda expressions and numbers are self-evaluating in Scheme-1,
so after the calls to EVAL-1, we are effectively saying

	(apply-1 '(lambda (x) (+ x 3)) '(5))

APPLY-1 will substitute 5 for X in the body of the
lambda, giving the expression (+ 5 3), and calls EVAL-1
with that expression as argument.  This, too, is a procedure call.
EVAL-1 calls itself recursively to evaluate
the symbol + and the numbers 5 and 3.  The numbers are self-evaluating;
EVAL-1 evaluates symbols by using STk's EVAL, so it gets the primitive
addition procedure.  Then it calls APPLY-1 with that procedure and
the list (5 3) as its arguments.  APPLY-1 recognizes that the addition
procedure is primitive, so it calls STk's APPLY, which does the
actual addition.


(b) As another example, here's FILTER:

((lambda (f seq)
   ((lambda (filter) (filter filter pred seq))
    (lambda (filter pred seq)
      (if (null? seq)
	  '()
	  (if (pred (car seq))
	      (cons (car seq) (filter filter pred (cdr seq)))
	      (filter filter pred (cdr seq)))))))
 even?
 '(5 77 86 42 9 15 8))


(c) Why doesn't STk's map work in Scheme-1?  It works for primitives:

	Scheme-1: (map first '(the rain in spain))
	(t r i s)

but not for lambda-defined procedures:

	Scheme-1: (map (lambda (x) (first x)) '(the rain in spain))
	Error: bad procedure: (lambda (x) (first x))

This problem illustrates the complexity of having two Scheme interpreters
coexisting, STk and Scheme-1.  In Scheme-1, lambda expressions are
self-evaluating:

	Scheme-1: (lambda (x) (first x))
	(lambda (x) (first x))

But in STk, lambda expressions evaluate to procedures, which are a different
kind of thing:

	STk> (lambda (x) (first x))
	#[closure arglist=(x) 40179938]

STk's MAP function requires an *STk* procedure as its argument, not a Scheme-1
procedure!  Scheme-1 uses STk's primitives as its primitives, so MAP is happy
with them.  But a Scheme-1 lambda-defined procedure just isn't the same thing
as an STk lambda-defined procedure.