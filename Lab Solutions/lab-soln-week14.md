LAB:
----

4.27  Lazy vs. mutation

The first time you type COUNT you get 1; the second time you get 2.
Why?  When you say
	(define w (id (id 10)))
the DEFINE special form handler eval-definition EVALs its second
argument (id (id 10)).  Given an application, EVAL calls APPLY
to invoke ID for the outer invocation, but the inner invocation
is providing an argument to a compound procedure, so it's delayed.
That's why COUNT is 1 -- the outer call to ID has actually happened,
but not the inner one.

The value of W is therefore a promise to compute (id 10), since
ID returns its argument.  When you ask the evaluator to print W,
that promise is fulfilled, and so COUNT becomes 2.


4.29  Memoizing or not

You'd expect a program that uses the same argument repeatedly to
be most strongly affected.  For example, I wrote

(define (n-copies n stuff)
  (if (= n 0)
      '()
      (cons stuff (n-copies (- n 1) stuff))))

Then if you use n-copies with something requiring a fair amount
of computation, such as

(n-copies 6 (factorial 7))

you can see a dramatic difference.

About their square/id example, remember to (set! count 0) before
each experiment.  Then the memoizing version leaves count at 1,
whereas the non-memoizing version sets count to 2.



4.35 an-integer-between

(define (an-integer-between low high)
  (if (> low high)
      (amb)
      (amb low (an-integer-between (+ low 1) high))))


4.38 adjacent floors

Remove the line (require (not (= (abs (- smith fletcher)) 1)))


[The continuation part of the lab was just try-this.]
