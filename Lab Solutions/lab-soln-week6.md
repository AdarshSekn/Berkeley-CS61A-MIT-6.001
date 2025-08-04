LAB EXERCISES:

2.25.  Extract 7

(cadr (caddr '(1 3 (5 7) 9)))

I did that one by knowing that "cadr" means "the second element" and
"caddr" means "the third element," and the seven is the second element
of the third element of the overall list.

(car (car '((7)))

(cadr (cadr (cadr (cadr (cadr (cadr '(1 (2 (3 (4 (5 (6 7))))))))))))



2.53.  Finger exercises.   
Note that it matters how many parentheses are printed!

> (list 'a 'b 'c)
(a b c)

> (list (list 'george))
((george))

> (cdr '((x1 x2) (y1 y2)))
((y1 y2))

> (cadr '((x1 x2) (y1 y2)))
(y1 y2)

> (pair? (car '(a short list)))
#f

> (memq 'red '((red shoes) (blue socks)))
#f

> (memq 'red '(red shoes blue socks))
(red shoes blue socks)



2.55 (car ''abracadabra)

When you write

    'foo

it's just an abbreviation for

    (quote foo)

no matter what foo is, and no matter what the context is.  So

    ''foo

is an abbreviation for

    (quote (quote foo))

If you enter the expression

    (car ''abracadabra)

you are really saying

    (car (quote (quote abracadabra)))

Using the usual evaluation rules, we start by evaluating the subexpressions.
The symbol car evaluates to a function.  The expression

    (quote (quote abracadabra))

evaluates to the unevaluated argument to (the outer) quote, namely

    (quote abracadabra)

That latter list is the actual argument to car, and so car returns the first
element of that list, i.e., the word quote.


Another example:

    (cdddr '(this list contains '(a quote)))

is the same as

    (cdddr '(this list contains (quote (a quote))))

which comes out to

    ((quote (a quote)))


P.S.:  Don't think that (car ''foo) is a quotation mark!  First of all,
the quotation mark has already been turned into the list for which it
is an abbreviation before we evaluate the CAR; secondly, even if the
quotation mark weren't an abbreviation, CAR isn't FIRST, so it doesn't
take the first character of a quoted word!



2.27.  Deep-reverse.

This is a tough problem to think about, although you can write a really
simple program once you understand how.  One trick is to deep-reverse a
list yourself, by hand, without thinking about it too hard, and THEN ask
yourself how you did it.  It's pretty easy for you to take a list like

((1 2 3) (4 5 6) (7 8 9))

and instantly write down

((9 8 7) (6 5 4) (3 2 1))

How'd you do it?  The answer probably is, "I reversed the list and then I
deep-reversed each of the sublists."  So:

(define (deep-reverse lst)                  ;; Almost working version
  (map deep-reverse (reverse lst)))

But this doesn't QUITE work, because eventually you get down to the level
of atoms (symbols or numbers) and you can't map over an atom.  So:

(define (deep-reverse lst)
  (if (pair? lst)
      (map deep-reverse (reverse lst))
      lst))

If you tried to define deep-reverse without using map, you'll appreciate
the intellectual power it gives you.  You probably got completely lost in
cars and cdrs, none of which are used in this program.

Now that you understand the algorithm, it's possible to do what the problem
asked us to do, namely "modify your reverse procedure":

(define (deep-reverse lst)
  (define (iter old new)
    (cond ((null? old) new)
	  ((not (pair? old)) old)
	  (else (iter (cdr old) (cons (deep-reverse (car old)) new)))))
  (iter lst '()))

This program will repay careful study, especially if you've fallen into the
trap of thinking that there is an iterative form and a recursive form in which
any problem can be expressed.  Deep-reverse combines two subproblems.  The
top-level reversal is one that can naturally be expressed iteratively, and
in this procedure the invocation of iter within itself does express an
iteration.  But the deep-reversal of the sublists is an inherently recursive
problem; there is no way to do it without saving a lot of state information
at each level of the tree.  So the call to deep-reverse within iter is truly
recursive, and necessarily so.  Can you express the time and space requirements
of this procedure in Theta(...) notation?


5.  Scheme-1 AND form.

Special forms are handled by clauses in the COND inside EVAL-1, so we
start by adding one for this new form:

(define (eval-1 exp)
  (cond ((constant? exp) exp)
	((symbol? exp) (error "Free variable: " exp))
	((quote-exp? exp) (cadr exp))
	((if-exp? exp)
	 (if (eval-1 (cadr exp))
	     (eval-1 (caddr exp))
	     (eval-1 (cadddr exp))))
	((lambda-exp? exp) exp)
	((AND-EXP? EXP) (EVAL-AND (CDR EXP)))	;; added
	((pair? exp) (apply-1 (car exp)
			      (map eval-1 (cdr exp))))
	(else (error "bad expr: " exp))))

Note that the new clause has to come before the PAIR? test, because special
forms are also pairs, and must be caught before we try to interpret them as
ordinary procedure calls.

We also need the helper that checks for a list starting with the word AND:

(define and-exp? (exp-checker 'and))

That was the easy part.  Now we have to do the actual work, in the
procedure EVAL-AND.  I chose to give it (CDR EXP) as its argument because
I'm envisioning a recursive loop through the subexpressions, and we want
to leave out the word AND itself, which isn't to be evaluated.

What AND is supposed to do is to go through the subexpressions from left
to right, evaluating each in turn until either some expression's value is
#F (in which case we return #F) or we run out (in which case we return,
to get exactly Scheme's behavior, the value of the last expression, which
might be some true value other than #T).

(define (eval-and subexps)
  (if (null? subexps)				; Trivial case: (AND)
      #T					;  returns #T
      (let ((result (eval-1 (car subexps))))	; else eval first one.
	(cond ((null? (cdr subexps)) result)	; Last one, return its value.
	      ((equal? result #F) #F)		; False, end early.
	      (else (eval-and (cdr subexps))))))) ; else do the next one.

The LET here is used so that there is only one recursive call to EVAL-1,
but the program can be written without it, and turns out only to call
EVAL-1 once anyway, even though the call appears in two different places
in the code, because only one of them will be carried out (per invocation
of EVAL-AND, of course).

(define (eval-and subexps)
  (cond ((null? subexps) #T)
	((null? (cdr subexps)) (eval-1 (car subexps)))
	((equal? (eval-1 (car subexps)) #F) #F)
	(else (eval-and (cdr subexps)))))

Note that the first NULL? test is not really a base case; unless the
entire expression given to us was exactly (AND), the second NULL? test
will always become true before the first one does.  It's that second
one that's the base case.

(If we wanted AND always to return either #T or #F, rather than return
the value of the last expression, then we'd leave out the second NULL?
test, and the first one *would* be the base case of the recursion.)