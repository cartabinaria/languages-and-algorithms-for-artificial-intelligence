# Module 3 - 2026-06-15 exam

The solutions to the multiple choice questions are provided by the professor.
The solutions to the problems, typeset by Stefano Volpe, are based on the
professor's feedback for another student. Use with care!

## Multiple choice questions

### Question 1

**C.** Recall that the set of all possible strings has the same cardinality
as $\mathbb{N}$. We observe that:

-  $|\mathbb{N}| < |\mathbb{R}| \leq | \mathbb{R}^2 | = | \mathbb{C} |$;
-  $|\mathbb{N}| < |\mathbb{R}| \leq | \mathbb{R}^3 |$;
-  $|\mathbb{N}| = |\mathbb{Q}| = | \mathbb{Q}^2 |$.

### Question 2

**A and B.** It suffices to count the states of the former, of the latter, and
then compare them. This is done in linear time, so the problem is in P, and
hence also in NP and EXP.

### Question 3

**A and C.**

### Question 4

**B and C.** A does not hold, because the algorithm might be incorrect, or it
might be needlessly inefficient. B holds, as we have no proof that such
algorithms cannot exist (in fact, we already have examples of these). C holds,
because it is already a know fact. D does not hold, because the statement says
"space", not "time", so it has nothing to do with P.

### Question 5

**C and D**. The VC-dimension must be at least 2, since ${1,2}$ can be
shattered by $\{[0;0],[1;1],[2;2],[1;2]\}$. The VC-dimension cannot more than 2,
because we can order any three distinct real numbers as $x < y < z$. Once, we
do, we realize that no close interval can include $x$ and $z$ but not $y$. So
the VC-dimension must be exactly 2 (D holds), so the representation class is
efficiently PAC-learnable (C holds). Hence, it is not infinite (A does
not hold). The axis-aligned rectangles' VC-dimension, on the other hand, is at
least 3, since $\{(0,0),(2,0),(1,2)\}$ can be easily shattered using 8 appropriate
rectangles (B does not hold).

## Problems

### Problem 1

Let us consider a machine with two tapes and states $Q = \{odd,even,final\}$,
where "odd" is the initial state, and "final" is the final one. We don't need
auxiliary tape symbols. We only specify the transition function on some inputs.
Its output on the other inputs is irrelevant:

- at state "odd":
  - if we are reading a blank on the input tape, we write a 1 on the
    input/output tape, do not move any heads, and progress to the final state;
  - if we are reading another symbol, we write blank on the input/output tape,
    move the input head right, and progress to the "even" state;
- at state "even":
  - if we are reading a blank on the input tape, we write a 1 on the
    input/output tape, do not move any heads, and progress to the final state;
  - if we are reading a 0 on the input tape, we write 0 on the input/output
    tape, do not move any heads, and progress to the final state;
  - if we are reading a 1 on the input tape, we write blank on the input/output
    tape, move the input head right, and progress to the "odd" state.

At the end of the execution, a 1 on the input/output tape means we accepted the
string. A 0 means we rejected it. The time complexity is linear, because at
every reachable configuration we either move the input head right, or we move to
the final state.

### Problem 2

Given input $n$, we:

1. nondeterministically choose $2 \leq a < n$;
2. if $a$ is not prime, we reject;
3. nondeterministically choose $2 \leq b < n$;
4. if $b$ is not prime, we reject;
5. nondeterministically choose $1 \leq x < n$;
6. nondeterministically choose $1 \leq y < n$;
7. accept if and only if $n = a^x b^y$.

Each step is in polytime:

- all nondeterministic choices have a branching factor below $n$, so they
  can be emulated with binary nondeterministic choices in polytime;
- we assumed the primality decider to be polytime;
- product and exponentials of natural numbers are also polytime.

### Problem 3

This variation is in P. The following greedy polytime algorithm witnesses it:

1. sort objects by decreasing value;
2. accumulate from left to right weights and values in two different counters,
   applying the following checks after each item:
   1. if the accumulated value is greater than $k$, return true;
   2. else, if the accumulated weight is not less than $z$, return false;
3. return false.

The algorithm is correct: if a solution of $a$ objects exists, then the $a$ most
valuable objects must also be a solution, and so the algorithms returns true
after at most $a$ steps (possibly less). If a solution does not exist, the
algorithm will fail after trying to construct one from the most valuable
objects.

The algorithm is polytime. Indeed, step 1 and 3 clearly are. So is step 2, since
the number of iterations is bounded by the length of the vector, and the
operation executed at each iteration is polytime.
