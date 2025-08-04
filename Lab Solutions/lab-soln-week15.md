LAB
===

4.55

(supervisor ?x (Bitdiddle Ben))

(job ?x (accounting . ?y))

(address ?x (Slumerville . ?y))

The dots are needed because (accounting ?y), for example, would match
only entries in which there was a single element after the word "accounting."
That is, (accounting ?y) would match (accounting scrivener) but not
(accounting chief accountant).


4.62
The base case here involves a 1-element list, not the empty list.

(rule (last-pair (?x) (?x)))

(rule (last-pair (?y . ?z) ?x)
      (last-pair ?z ?x))
