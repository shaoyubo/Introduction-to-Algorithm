# Chapter 9. Medians and Order Statistics

The ith order statistics of a set of n elements in the ith smallest element. A median, informally, is the "halfway point" of the set. When n is odd, the median is unique, occurring at i = (n + 1)/2. When n is even, there are two medians, occurring at i = n/2 and i = n/2 + 1. Thus, regardless of the parity of n, medians occur at i = &lfloor;(n + 1)/2&rfloor; (the lower median) and i = &lceil;(n + 1)/2&rceil; (th upper median).

This chapter addresses the problem of selecting the ith order statistic from a set of n distinct numbers. We assume for convenience that the set contains distinct numbers, although virtually everything that we do extends to the situation in which a set contains repeated values. We formally specify the selection problem as follows:

> Input: A set A of n (distinct) numbers and an integer i, with 1 &le; i &le; n.

> Output: The element x &in; A that is larger than exactly i - 1 other elements of A.

We can solve the selection problem in O(nlg n) time, since we can sort the nubmers using heapsort or merge sort and then simply index the ith element in the output array. This chapter presents faster algorithms.

## 9.1 Minimum and Maximum

How many comparisons are necessary to determine the minimum of a set of n elements. We can easily obtain an upper bound of n - 1 comparisons: examine each element of the set in turn and keep track the smallest element seen so far. In the following procedure, we assume that the set resides in array A, where A.length = n.

```
MINIMUM(A)
	min = A[1]
	for i = 2 to A.length
		if min > A[i]
			min = A[i]
	return min
```

We can, of course, find the maximum with n - 1 comparisons as well.

**Simultaneous minimum and maximum**

In fact, we can find both the minimum and the maximum using at most 3&lfloor;n/2&rfloor; comparisons. We do so by maintaining both the maximum and minimum elements seen thus far. Rather than processing each element of the input by comparing it against the current minimum and maximum, at a cost of 2 comparisons per element, we process elements in pairs. We compare pairs if elements from the input first with each other, and then we compare the smaller with the current minimum and the larger to the current maximum, at a cost of 3 comparisons for every 2 elements. 

Let us analyze the total number of comparisons. If n is odd, then we perform 3&lfloor;n/2&rfloor; comparisons. If n is even, we perform 1 initial comparison followed by 3(n - 2)/2 comparisons, for a total of 3n/2 - 2. Thus, in either case, the total number of comparisons is at most 3&lfloor;n/2&rfloor;.



