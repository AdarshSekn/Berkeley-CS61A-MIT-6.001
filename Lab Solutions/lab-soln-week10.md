LAB ASSIGNMENT:

3.12 append vs. append!  

exp1 is (b); exp2 is (b c d).  Append (without the !) makes copies of the
two pairs that are part of the list x.  (You can tell because it uses
cons, which is the constructor function that generates a brand new pair.)
Append! does not invoke cons; it mutates the existing pairs to combine
the two argument lists.


2.  Set! vs. set-cdr!

There are two ways to think about this, and you should understand both
of them:

The syntactic explanation -- SET! is a special form; its first argument
must be a symbol, not a compound expression.  So anything of the form
       (set! (...) ...)
must be an error.

The semantic explanation -- SET! and SET-CDR! are about two completely
different purposes.  SET! is about the bindings of variables in an
environment.  SET-CDR! is about pointers within pairs.  SET! has nothing
to do with pairs; SET-CDR! has nothing to do with variables.  There is
no situation in which they are interchangeable.

(Note:  The book says, correctly, that the two are *equivalent* in the
sense that you can use one to implement the other.  But what that means
is that, for example, if we didn't have pairs in our language we could
use the oop techniques we've learned, including local state variables
bound in an environment, to simulate pairs.  Conversely, we'll see in
Chapter 4 that we can write a Scheme interpreter, including environments
as an abstract data type, building them out of pairs.  But given that
we are using the regular Scheme's built-in pairs and built-in environments,
those have nothing to do with each other.)



3a.  Fill in the blanks.

> (define list1 (list (list 'a) 'b))
list1
> (define list2 (list (list 'x) 'y))
list2
> (set-cdr! ____________ ______________)
okay
> (set-cdr! ____________ ______________)
okay
> list1
((a x b) b)
> list2
((x b) y)

The key point here is that if we're only allowed these two SET-CDR!s then
we'd better modify list2 first, because the new value for list1 uses the
sublist (x b) that we'll create for list2.

So it's

(set-cdr! (car list2) (cdr list1))

(set-cdr! (car list1) (car list2))



3b.  Now do (set-car! (cdr list1) (cadr list2)).

Everything that used to be "b" is now "y" instead:

> list1
((a x y) y)
> list2
((x y) y)

The reason is that there was only one appearance of the symbol B in
the diagram, namely as the cadr of list1; every appearance of B in the
printed representation of list1 or list2 came from pointers to the
pair (cdr list1).  The SET-CAR! only makes one change to one pair,
but three different things point (directly or indirectly) to it.



3.13 make-cycle

The diagram is

     +----------------+
     |                |
     V                |
---> XX--->XX--->XX---+
     |     |     |
     V     V     V
     a     b     c

(last-pair z) will never return, because there is always a non-empty
cdr to look at next.



3.14  Mystery procedure.

This procedure is REVERSE!, that is to say, it reverses the list
by mutation.  After

     (define v (list 'a 'b 'c 'd))
     (define w (mystery v))

the value of w is the list (d c b a); the value of v is the list (a)
because v is still bound to the pair whose car is a.  (The procedure
does not change the cars of any pairs.)



5a.  We want Scheme-2 to accept both the ordinary form
	(define x 3)
and the procedure-abbreviation form
	(define (square x) (* x x))
The latter should be treated as if the user had typed
	(define square (lambda (x) (* x x)))
The hint says we can use data abstraction to achieve this.

Here is the existing code that handles DEFINE:

(define (eval-2 exp env)
  (cond ...
	((define-exp? exp) (put (cadr exp)
				(eval-2 (caddr exp) env)
				env)
	 		   'okay)
	...))

We're going to use selectors for the pieces of the DEFINE expression:

(define (eval-2 exp env)
  (cond ...
	((define-exp? exp) (put (DEFINE-VARIABLE exp)
				(eval-2 (DEFINE-VALUE exp) env)
				env)
	 		   'okay)
	...))

To get the original behavior we would define the selectors this way:

(define define-variable cadr)
(define define-value caddr)

But instead we'll check to see if the cadr of the expression is a
symbol (so we use the ordinary notation) or a list (abbreviating
a procedure definition):

(define (define-variable exp)
  (if (pair? (cadr exp))
      (caadr exp)		;(define (XXXX params) body)
      (cadr exp)))

(define (define-value exp)
  (if (pair? (cadr exp))
      (cons 'lambda
	    (cons (cdadr exp)	;params
		  (cddr exp)))	;body
      (caddr exp)))

Writing selectors like this is the sort of situation in which the compositions
like CAADR are helpful.  That particular one is (car (cadr exp)), which is the
first element of the second element of the expression.  (You should recognize
CADR, CADDR, and CADDDR as selectors for the second, third, and fourth
elements of a list.)  The second element of the expression is a list such as
(SQUARE X), so the car of that list is the variable name.

Since DEFINE-VALUE is supposed to return an expression, we have to construct
a LAMBDA expression, making explicit what this notation abbreviates.


5c.  In a procedure call, parameters are processed from left to right,
and PUT adds each parameter to the front of the environment.  So they
end up in reverse order.  Similarly, top-level DEFINEs add things to
the global environment in reverse order.  So the sequence of expressions
should be

Scheme-2: (define b 2)
Scheme-2: (define a 1)
Scheme-2: ((lambda (c b) 'foo) 4 3)

It doesn't matter what's in the body of the procedure, since we're
interested in the environments rather than in the values returned.
