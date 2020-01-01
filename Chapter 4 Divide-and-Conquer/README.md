# Chapter 4. Divide-and-Conquer

## 4.1 The maximum-subarray problem

Suppose that you been offered the opportunity to invest in the Volatile Chemical Corporation. Like the checmicals the company produces, the stock price of the Volatile Chemical Corporation is rather volatile. You are allowed to buy one unit of stock only one time and then sell it at a later date, buying and selling after the close of trading for the day. To compensate for this restriction, you are allowed to learn what the price of the stock will be in the future. You goal is to maximize your profit.

**A brute-force solution**

Try every possible pair of buy and sell dates in which the buy date precedes the sell date. A period of n days has n choose 2 such pairs of dates. And the approach would take &Omega;(n<sup>2</sup>) time.

**A solution using divide-and-conquer**

Suppose we want to find a maximum subarray of the subarray A[low .. high]. Divide-and-conquer suggests that we divide the subarray into two subarrays of as equal size as possible. That is, we find the midpoint, say mid, of the subarray, and consider the subarrays A[low .. mid] and A[mid+1 .. high]. 

The procedure FIND-MAX-CROSS-SUBARRAY (&Theta;(n) time) takes as input the array A and the indices low, mid, and high, and it returns a tuple containing the indices demarcating a maximum subarray that crosses the midpoint, along with the sum of the values in a maximum subarray.

```
FIND-MAX-CROSS-SUBARRAY(A, low, mid, high)
	left-sum = Integer.MIN_VALUE
	sum = 0
	for i = mid downto low
		sum = sum + A[i]
		if sum > left-sum
			left-sum = sum
			max-left = i
	right-sum = Integer.MIN_VALUE
	sum = 0
	for j = mid + 1 to high
		sum = sum + A[j]
		if sum > right-sum
			right-sum = sum
			max-right = j
	return (max-left, max-right, left-sum + right-sum)
```

With a linear-time FIND-MAX-CROSS-SUBARRAY procedure in hand, we can write pseudocode for a divide-and-conquer algorithm to solve the maximum-subarray problem:

```
FIND-MAXIMUM-SUBARRAY(A, low, high)
	if high == low		// base case: only one element
		return (low, high, A[low])
	else 
		mid = Math.floor((low + high) / 2)
		(left-low, left-high, left-sum) = FIND-MAXIMUM-SUBARRAY(A, low, mid)
		(right-low, right-high, right-sum) = FIND-MAXIMUM-SUBARRAY(A, mid + 1, high)
		(cross-low, cross-high, cross-sum) = FIND-MAX-CROSS-SUBARRAY(A, low, mid, high)
		if left-sum >= right-sum and left-sum >= cross-sum
			return (left-low, left-high, left-sum)
		else if right-sum >= left-sum and right-sum >= cross-sum
			return (right-low, right-high, right-sum)
		else
			return (cross-low, cross-high, cross-sum)
```

**Analyzing the divide-and-conquer algorithm**

A recurrence for the running time T(n) of FIND-MAXIMUM-SUBARRAY: T(n) = &Theta;(1) if n = 1, T(n) = 2T(n/2) + &Theta;(n) if n > 1. And the solution for T(n) is &Theta;(nlgn).

## 4.2 Strassen's algorithm for matrix multiplication

If A = (a<sub>ij</sub>) and B = (b<sub>ij</sub>) are square n &times; n matrices, then in the product C = A &sdot; B, we define the entry c<sub>ij</sub>, for i, j = 1,2 ,..., n, by c<sub>ij</sub> = &sum;<sub>k=1</sub><sup>n</sup>a<sub>ik</sub>&sdot;b<sub>kj</sub>.

The following procedure takes n &times; n matrices A and B and multiplies them, returning their n &times; n product C. We assume that each matrix has an attribute rows, giving the number of rows in the matrix.

```
SQUARE-MATRIX-MULTIPLY(A, B)
	n = A.rows
	let C be a new n * n matrix
	for i = 1 to n
		for j = 1 to n
			cij = 0
			for k = 1 to n
				cij = cij + aik * bkj
	return C
```

The SQUARE-MATRIX-MULTIPLY procedure takes &Theta;(n<sup>3</sup>).

**A simple divide-and-conquer algorithm**

Suppose that we partition each of A, B, and C into four n/2 &times; n/2 matrices and we could obtain the following four equations:

>C<sub>11</sub> = A<sub>11</sub> &sdot; B<sub>11</sub> + A<sub>12</sub> &sdot; B<sub>21</sub>.

>C<sub>12</sub> = A<sub>11</sub> &sdot; B<sub>12</sub> + A<sub>12</sub> &sdot; B<sub>22</sub>.

>C<sub>21</sub> = A<sub>21</sub> &sdot; B<sub>11</sub> + A<sub>22</sub> &sdot; B<sub>21</sub>.

>C<sub>22</sub> = A<sub>21</sub> &sdot; B<sub>12</sub> + A<sub>22</sub> &sdot; B<sub>22</sub>.

Then we could use these equations to create a straightforward, recursive, divide-and-conquer algorithm:

```
SQUARE-MATRIX-MULTIPLY-RECURSIVE(A, B)
	n = A.rows
	let C be a new n * n matrix
	if n == 1
		c11 = a11 * b11
	else
		partition A, B, and C 
		C11 = SQUARE-MATRIX-MULTIPLY-RECURSIVE(A11, B11) + SQUARE-MATRIX-MULTIPLY-RECURSIVE(A12, B21)
		C12 = SQUARE-MATRIX-MULTIPLY-RECURSIVE(A11, B12) + SQUARE-MATRIX-MULTIPLY-RECURSIVE(A12, B22)
		C21 = SQUARE-MATRIX-MULTIPLY-RECURSIVE(A21, B11) + SQUARE-MATRIX-MULTIPLY-RECURSIVE(A22, B21)
		C22 = SQUARE-MATRIX-MULTIPLY-RECURSIVE(A21, B12) + SQUARE-MATRIX-MULTIPLY-RECURSIVE(A22, B22)
	return C
```

Thus, the recurrence for the running time of SQUARE-MATRIX-MULTIPLY-RECURSIVE is T(n) = &Theta;(1) if n = 1, T(n) = 8T(n/2) + &Theta;(n<sup>2</sup>) if n > 1. And the running time for T(n) = &Theta;(n<sup>3</sup>).

**Strassen's method**

Four steps:

1. Divide the input matrices A and B and output matrix C into n/2 &times; n/2 submatrices. This step take &Theta;(1) time by index calculation, just as in SQUARE-MATRIX-MULTIPLY-RECURSIVE.

2. Create 10 matrices S<sub>1</sub>, S<sub>2</sub>,..., S<sub>10</sub>, each of which is n/2 &times; n/2 and is the sum or difference of two matrices created in step 1. We can create all 10 matrices in &Theta;(n<sup>2</sup>) time.

3. Using the submatrices created in step 1 and the 10 matrices created in step 2, recursively compute seven matrix products P<sub>1</sub>, P<sub>2</sub>,..., P<sub>7</sub>. Each matrix P<sub>i</sub> is n/2 &times; n/2.

4. Compute the desired submatrices C<sub>11</sub>, C<sub>12</sub>, C<sub>21</sub>, C<sub>22</sub> of the result matrix C by adding and subtracting various combinations of the P<sub>i</sub> matrices. We can compute all four submatrices in &Theta;(n<sup>2</sup>) time.

Then we can obtain the following recurrence for the running time T(n) of Strassen's algorithm: T(n) = &Theta;(1) if n = 1, T(n) = 7T(n/2) + &Theta;(n<sup>2</sup>) if n > 1. And by the master method, this recurrence has the solution T(n) = &Theta;(n<sup>lg7</sup>).

In step 2, we create the following 10 matrices:

> S<sub>1</sub> = B<sub>12</sub> - B<sub>22</sub>,

> S<sub>2</sub> = A<sub>11</sub> + A<sub>12</sub>,

> S<sub>3</sub> = A<sub>21</sub> + A<sub>22</sub>,

> S<sub>4</sub> = B<sub>21</sub> - B<sub>11</sub>,

> S<sub>5</sub> = A<sub>11</sub> + A<sub>22</sub>,

> S<sub>6</sub> = B<sub>11</sub> + B<sub>22</sub>,

> S<sub>7</sub> = A<sub>12</sub> - A<sub>22</sub>,

> S<sub>8</sub> = B<sub>21</sub> + B<sub>22</sub>,

> S<sub>9</sub> = A<sub>11</sub> - A<sub>21</sub>,

> S<sub>10</sub> = B<sub>11</sub> + B<sub>12</sub>.

In step 3, we recursively mutiply n/2 &times; n/2 matrices seven times to compute the following n/2 &times; n/2 matrices, each of which is the sum or difference of products of A and B submatrices:

> P<sub>1</sub> = A<sub>11</sub> &sdot; S<sub>1</sub>,

> P<sub>2</sub> = S<sub>2</sub> &sdot; B<sub>22</sub>,

> P<sub>3</sub> = S<sub>3</sub> &sdot; B<sub>11</sub>,

> P<sub>4</sub> = A<sub>22</sub> &sdot; S<sub>4</sub>,

> P<sub>5</sub> = S<sub>5</sub> &sdot; S<sub>6</sub>,

> P<sub>6</sub> = S<sub>7</sub> &sdot; S<sub>8</sub>,

> P<sub>7</sub> = S<sub>9</sub> &sdot; S<sub>10</sub>.

In step 4, we add and subtract the P<sub>i</sub> matrices created in step 3 to constuct the four n/2 &times; n/2 submatrices of the product C. 

> C<sub>11</sub> = P<sub>5</sub> + P<sub>4</sub> - P<sub>2</sub> + P<sub>6</sub>,

> C<sub>12</sub> = P<sub>1</sub> + P<sub>2</sub>,

> C<sub>21</sub> = P<sub>3</sub> + P<sub>4</sub>,

> C<sub>22</sub> = P<sub>5</sub> + P<sub>1</sub> - P<sub>3</sub> - P<sub>7</sub>.

## 4.3 The substitution method for solving recurrences

The substitution method for solving recurrences comprises two steps:

1. Guess the form of the solution.

2. Use mathematical induction to find the constants and show that the solution works.


## 4.4 The recursion-tree method for solving recurrences

In a recursion tree, each node represents the cost of a single subproblem somewhere in the set of recursive function invocations. We sum the costs within each level of the tree to obtain a set of per-level costs, and then we sum all the per-level costs to determine the total cost of all levels of the recursion.

## 4.5 The master method for solving recurrences

**Theorem 4.1 (Master theorem)**

Let a &ge; 1 and b &ge; 1 be constants, let f(n) be a function, and let T(n) be defined on the nonnegative integers by the recurrence

> T(n) = aT(n/b) + f(n),

where we interpret n/b to mean either &lfloor;n/b&rfloor; or &lceil;n/b&rceil;. Then T(n) has the following asymptotic bounds:

1. If f(n) = O(n<sup>log<sub>b</sub>a - &epsilon;</sup>) for some constant &epsilon; > 0, then T(n) = &Theta;(n<sup>log<sub>b</sub>a</sup>).

2. If f(n) = &Theta;(n<sup>log<sub>b</sub>a</sup>), then T(n) = &Theta;(n<sup>log<sub>b</sub>a</sup>lgn).
 
3. If f(n) = &Omega;(n<sup>log<sub>b</sub>a + &epsilon;</sup>) for some constant &epsilon; > 0, and if af(n/b) &le; cf(n) for some constant c < 1 and all sufficiently large n, then T(n) = &Theta;(f(n)).

## 4.6 Proof of the master theorem

### 4.6.1 The proof for exact powers

**Lemma 4.2**

Let a &ge; 1 and b > 1 be constants, and let f(n) be a nonnegative function defined on exact powers of b. Define T(n) on exact powers of b by the recurrence T(n) = aT(n/b) + f(n) if n = b<sup>i</sup>, T(n) = &Theta;(1) if n = 1, where i is a positive integer. Then

> T(n) = &Theta;(n<sup>log<sub>b</sub>a</sup>) + &sum;<sub>j = 0</sub><sup>log<sub>b</sub>n-1</sub>a<sup>j</sup>f(n/b<sup>j</sup>).
















