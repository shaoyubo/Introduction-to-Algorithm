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
```






