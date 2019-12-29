# Chapter 3. Growth of Functions

## 3.1 Asymptotic notation

**Asymptotic notation, functions, and running times**

We will use asymptotic notation primarily to describe the running times of algorithms. Asymptotic notation actually applies to functions.

**&Theta;-notation**

For a given function g(n), we denote by &Theta;(g(n)) the set of functiuons

>&Theta;(g(n)) = {f(n): there exist positive constants c<sub>1</sub>, c<sub>2</sub>, and n<sub>0</sub> such that 0 <= c<sub>1</sub>g(n) <= f(n) <= c<sub>2</sub>g(n) for all n >= n<sub>0</sub>}.

**O-notation**

The &Theta;-notation asymptotically bounds a function from above and below. When we have only an asymptotic upper bound, we use O-notation.

For a given function g(n), we denote by O(g(n)) the set of functiuons

>O(g(n)) = {f(n): there exist positive constants c and n<sub>0</sub> such that 0 <= f(n) <= cg(n) for all n >= n<sub>0</sub>}.

**&Omega;-notation**

Just as O-notation provides an asymptotic upper bound on a function, &Omega;-notation provides an asymptotic lower bound. 

For a given function g(n), we denote by &Omega;(g(n)) the set of functiuons

>&Omega;(g(n)) = {f(n): there exist positive constants c and n<sub>0</sub> such that 0 <= cg(n) <= f(n) for all n >= n<sub>0</sub>}.

**Theorem 3.1**

>For any two functions f(n) and g(n), we have f(n) = &Theta;(g(n)) if and only if f(n) = O(g(n)) and f(n) = &Omega;(g(n)).

**o-notation*

We use o-notation to denote an upper bound that is not asymptotically tight. 

We formally define o(g(n)) as the set

>o(g(n)) = {f(n): for any positive constants c > 0, there exists a constant n<sub>0</sub> > 0 such that 0 <= f(n) < cg(n) for all n >= n<sub>0</sub>}.

