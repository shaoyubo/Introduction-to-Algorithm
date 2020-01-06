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

Let us analyze the total number of comparisons. If n is odd, then we perform 3&lfloor;n/2&rfloor; comparisons. If n is even, we perform 1 initial comparison followed by 3(n - 2)/2 comparisons, for a total of 3n/2 - 2. Thus, in either case, the total number of comparisons is at most 3&lfloor;n/2&rfloor;

## 9.2 Selection in expected linear time

RANDOMIZED-SELECT uses the procedure RANDOMIZED-PARTITION introduced in Section 7.3. Thus, like RANDOMIZED-QUICKSORT, it is a randomized algorithm, since its behavior is determined in part by the output of a random-number generator. The following code for RANDOMIZED-SELECT returns the ith smallest element of the array A[p .. r].

```
RANDOMIZED-SELECT(A, p, r, i)
	if p == r
		return A[p]
	q = RANDOMIZED-PARTITION(A, p, r)
	k = q - p + 1
	if i == k
		return A[q]
	elseif i < k
		return RANDOMIZED-SELECT(A, p, q - 1, i)
	else 
		return RANDOMIZED-SELECT(A, q + 1, r, i - k)
```

The worst-case running time for RANDOMIZED-SELECT is &Theta;(n<sup>2</sup>), even to find the minimum, because we could be extremely unlucky and always partition around the largest remaining element, and partitioning takes &Theta;(n) time. We will see that the algorithm has a linear expected running time, though, and because it is randomized, no particular input elicits the worst-case behabvior. Thus, we conclude that we can find any order statistic, and in particular the median, in expected linear time, assuming that the elements are distinct.

## 9.3 Selection in worst-case linear time

We now examine a selection algorithm whose running time is O(n) in the worst case. Like RANDOMIZED-SELECT, the algorithm SELECT finds the desired element by recursively partitioning the input array.

The SELECT algorithm determines the ith smallest of an input array of n > 1 distinct elements by executing the following steps. (If n = 1, then SELECT merely returns its only input value as the ith smallest.)

1. Divide the n elements of the input array into &lfloor;n/5&rfloor; groups of 5 elements each and at most one group made up of the remaining n mod 5 elements.

2. Find the median of each of the &lceil;n/5&rceil; by first insertion-sorting the elements of each group (of which there are at most 5) and then picking the median from the sorted list of group element.

3. Use SELECT recursively to find the median x of the &lceil;n/5&rceil; medians found in step 2. (If there are an even number of medians, then by our convntion, x is the lower median.)

4. Partition the input array around the median-of-medians x using the modified version of PARTITION. Let k be one more than the number of elements on the low side of the partition, so that x is the kth smallest element and there are n - k elements on the high side of the partition.

5. If i = k, then return x. Otherwise, use SELECT recursively to find the ith smallest element on the low side if i < k, or the (i - k)th smallest element on the high side if i > k.

The worst-case running time of SELECT is therefore linear. As in a comparison sort, SELECT and RANDOMIZED-SELECT determine information about the relative order of elements only by comparing elements. Recall from Chapter 8 that sorting requires &Omega;(nlg n) time in the comparison model, even on average. The linear-time sorting algorithms in Chapter 8 make assumptions in this chapter do not require any assumptions about the input. They are not suject to the &Omega;(nlg n) lower bound because they manage to solve the selection problem without sorting. Thus, solving the selection problem by sorting and indexing, as preseneted in the introduction to this chapter, is asymptotically inefficient.



