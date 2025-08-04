LAB EXERCISES:

1.  Error message hunt

+: not a number: foo
unbound variable: zot
eval: bad function in : (3)
too many arguments to: (bf 3 5)
random: bad number: -7
sqrt: number is negative: -6
Invalid argument to FIRST: ()
Argument to SENTENCE not a word or sentence:#f
define: bad variable name: 5

2.  Tracing

In a base-case call, the return value comes right after the call:

STk> (fib 5)
.. -> fib with n = 5
.... -> fib with n = 4
...... -> fib with n = 3
........ -> fib with n = 2
.......... -> fib with n = 1	<=== Here's a base case
.......... <- fib returns 1	<=== with its return value
.......... -> fib with n = 0
.......... <- fib returns 0
........ <- fib returns 1
........ -> fib with n = 1
........ <- fib returns 1
...... <- fib returns 2
...... -> fib with n = 2
........ -> fib with n = 1
........ <- fib returns 1
........ -> fib with n = 0
........ <- fib returns 0
...... <- fib returns 1
.... <- fib returns 3
.... -> fib with n = 3
...... -> fib with n = 2
........ -> fib with n = 1
........ <- fib returns 1
........ -> fib with n = 0
........ <- fib returns 0
...... <- fib returns 1
...... -> fib with n = 1
...... <- fib returns 1
.... <- fib returns 2
.. <- fib returns 5
5

I count eight base-case calls.