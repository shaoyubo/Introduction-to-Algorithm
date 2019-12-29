# Chapter 3. Growth of Functions

## 3.1 Asymptotic notation

**Asymptotic notation, functions, and running times**

We will use asymptotic notation primarily to describe the running times of algorithms. Asymptotic notation actually applies to functions.

**&Theta;-notation**

For a given function g(n), we denote by &Theta;(g(n)) the set of functiuons

>&Theta;(g(n)) = {f(n): there exist positive constants c<sub>1</sub>, c<sub>2</sub>, and n<sub>0</sub> such that 0 &le; c<sub>1</sub>g(n) &le; f(n)&le; c<sub>2</sub>g(n) for all n &ge; n<sub>0</sub>}.

**O-notation**

The &Theta;-notation asymptotically bounds a function from above and below. When we have only an asymptotic upper bound, we use O-notation.

For a given function g(n), we denote by O(g(n)) the set of functiuons

>O(g(n)) = {f(n): there exist positive constants c and n<sub>0</sub> such that 0 &le; f(n) &le; cg(n) for all n &ge; n<sub>0</sub>}.

**&Omega;-notation**

Just as O-notation provides an asymptotic upper bound on a function, &Omega;-notation provides an asymptotic lower bound. 

For a given function g(n), we denote by &Omega;(g(n)) the set of functiuons

>&Omega;(g(n)) = {f(n): there exist positive constants c and n<sub>0</sub> such that 0 &le; cg(n) &le; f(n) for all n &ge; n<sub>0</sub>}.

**Theorem 3.1**

>For any two functions f(n) and g(n), we have f(n) = &Theta;(g(n)) if and only if f(n) = O(g(n)) and f(n) = &Omega;(g(n)).

**o-notation**

We use o-notation to denote an upper bound that is not asymptotically tight. 

We formally define o(g(n)) as the set

>o(g(n)) = {f(n): for any positive constants c, there exists a constant n<sub>0</sub> > 0 such that 0 &le; f(n) < cg(n) for all n &ge; n<sub>0</sub>}.

Intuitively, in o-notation, the function f(n) becomes insignificant relative to g(n) as n approaches infinity.

**&omega;-notation**

We define &omega;(g(n)) as the set

>&omega;(g(n)) = {f(n): for any positive constants c, there exists a constant n<sub>0</sub> > 0 such that 0 &le; cg(n) < f(n) for all n &ge; n<sub>0</sub>}.

In &omega;-notation, the function f(n) becomes significant relative to g(n) as n approaches infinity.

One way to define it is by f(n) &in; &omega;(g(n)) if and only if g(n) &in; o(f(n)).

**Comparing functions**

- Transitivity

>f(n) = &Theta;(g(n)) and g(n) = &Theta;(h(n)) imply f(n) = &Theta;(h(n)).

>f(n) = O(g(n)) and g(n) = O(h(n)) imply f(n) = O(h(n)).

>f(n) = &Omega;(g(n)) and g(n) = &Omega;(h(n)) imply f(n) = &Omega;(h(n)).

>f(n) = o(g(n)) and g(n) = o(h(n)) imply f(n) = o(h(n)).

>f(n) = &omega;(g(n)) and g(n) = &omega;(h(n)) imply f(n) = &omega;(h(n)).

- Reflexivity

>f(n) = &Theta;(f(n)).

>f(n) = O(f(n)).

>f(n) = &Omega;(f(n)).

- Symmetry

>f(n) = &Theta;(g(n)) if and only if g(n) = &Theta;(f(n)).

- Transpose symmetry

>f(n) = O(g(n)) if and only if g(n) = &Omega;(f(n)).

>f(n) = o(g(n)) if and only if g(n) = &omega;(f(n)).

- Trichotomy

> For any real numbers a and b, exactly one of the following must hold: a < b, a = b, a > b.

## 3.2 Standard notations and common functions

**Monotonicity**

>A function f(n) is monotonically increasing if m &le; n implies f(m) &le; f(n).

>A function f(n) is monotonically decreasing if m &le; n implies f(m) &ge; f(n).

>A function f(n) is strictly increasing if m &le; n implies f(m) < f(n).

>A function f(n) is strictly decreasing if m &le; n implies f(m) > f(n).

**Floors and ceilings**

For any real number x, we denote the greatest integer less than or equal to x by &lfloor;x&rfloor; and the least integer greater than or equal to x by &lceil;x&rceil;.

> For all real x, x - 1 < &lfloor;x&rfloor; &le; x &le; &lceil;x&rceil; < x + 1.

The floor function f(x) = &lfloor;x&rfloor; is monotonically increasing as is the ceiling function f(x) = &lceil;x&rceil;.

**Modular arithmetic**

For any integer a and any positive integer n, the value a mod n is the remainder (or residue) of the quotient a/n:

> a mod n = a - n &lfloor;a/n&rfloor;. 

It follows that 

> 0 &le; a mod n < n.

**Polynomials**

Given a nonegative integer d, a polynomial in n of degree d is a function p(n) of the form

> p(n) = &Sum;<sub>i=0</sub><sup>d</sup> a<sub>i</sub>n<sup>i</sup>,

where the constant a<sub>0</sub>, a<sub>1</sub>, ... , a<sub>d</sub> are the coefficients of the polynomial and a<sub>d</sub> &ne; 0.



**Exponentials**

**Lograithms**

**Factorials**

**Functional iteration**

**The iterated logarithm function**

**Fibonacci numbers**






