# Chapter 7. Quicksort

The quicksort algorithm has a worst-case running time of &Theta;(n<sup>2</sup>) on an input array of n numbers. Despite this slow worst-case running time, quicksort is often the best practical choice for sorting because it is remarkably efficient on the average: its expected running time is &Theta;(nlg n), and the constant factors hidden in the &Theta;(nlg n) notation are quite small.

## 7.1 Description of quicksort

Quicksort, like merge sort, applies the divide-and-conquer paradigm introduced in Section 2.3.1. Here is the three-step divide-and-conquer process for sorting a typical subarray A[p .. r]:

- Divide: Partition (rearrange) the array A[p .. r] into two (possibly empty) subarrays A[p .. q - 1] and A[q + 1 .. r] such that each element of A[p .. q - 1] is less than or equal to A[q], which is, in turn, less than or equal to each element of A[q + 1 .. r]. Compute the index q as part of this partitioning procedure.

- Conquer: Sort the two subarrays A[p .. q - 1] and A[q + 1 .. r] by recursive calls to quicksort.

- Combine: Because the subarrays are already sorted, no work is needed to combine them: the entire array A[p .. r] is now sorted.

The following procedure implements quicksort:

```
QUICKSORT(A, p, r)
	if p < r
		q = PARTITION(A, p, r)
		QUICKSORT(A, p, q - 1)
		QUICKSORT(A, q + 1, r)
```

To sort an entire array A, the initial call is QUICKSORT(A, 1, A.length).

**Partitioning the array**

The key to the algorithm is the PARTITION procedure, which rearranges the subarray A[p .. r] in place.

```
PARTITION(A, p, r)
	x = A[r]
	i = p - 1
	for j = p to r - 1
		if A[j] <= x
			i = i + 1
			exchange A[i] with A[j]
	exchange A[i + 1] with A[r]
	return i + 1
```

Then foor any array index k,

1. If p &le; k &le; i, then A[k] &le; x.

2. If i + 1 &le; k &le; j - 1, then A[k] > x.

3. If k = r, then A[k] = x.

The running time of PARTITION on the subarray A[p .. r] is &Theta;(n), where n = r - p + 1.

## 7.2 Performance of quicksort

The running time of quicksort depends on whether the partitioning is balanced or unbalanced, which in turn depends on which elements are used for partitioning. If the partitioning is balanced, the algorithm runs asymptotically as fast as merge sort. If the partitioning is unbalanced, however, it can run asymptotically as slowly as insertion sort. In this section, we shall informally investigate how quicksort performs under the assumptions of balanced versus unbalanced partitioning.

**Worst-case partitioning**

The worst-case behavior for quicksort occurs when the partitioning routine produces one subproblem with n - 1 elements and one with 0 elements. Then we get the recurrence T(n) = T(n - 1) + T(0) + &Theta;(n) = &Theta;(n<sup>2</sup>).  Thus, if the partitioning is maximally unbalanced at every recursive level of the algorithm, the running time is &Theta;(n<sup>2</sup>). Therefore, the worst-case running time of quicksort is no better than that of insertion sort.

**Best-case partitioning**

In the most even possible split, PARTITION produces two subproblems, each of size no more than n/2. In this case, quicksort runs much faster. The recurrence for the running time is then T(n) = 2T(n/2) + &Theta;(n) = &Theta;(nlg n). 

**Balanced partitioning**

The average-case running time of quicksort is much closer to the best case than to the worst case. For any split of constant proportionality yields a recursion tree of depth &Theta;(lg n), where the cost at each level is O(n). The running time is therefore O(nlg n) whenever the split has constant proportionally.


## 7.3 A randomized version of quicksort

In exploring the average-case behavior of quicksort, we have made an assumption that all permutations of the input numbers are equally likely. In section 5.3, we randomized our algorithm by explicitly permuting the input. We could do so for quicksort also, but a different randomization technique, called random sampling, yields a simpler analysis. Instead of always using A[r] as the pivot, we will select a randomly chosen element from the subarray A[p .. r]. 

In the new partition procedure, we simply implement the swap before actually partitioning:

```
RANDOMIZED-PARTITION(A, p, r)
	i = RANDOM(p, r)
	exchange A[r] with A[i]
	return PARTITION(A, p ,r)
```

The new quicksort calls RANDOMIZED-PARTITION in place of PARTITION:

```
RANDOMIZED-QUICKSORT(A, p, r)
	if p < r
		q = RANDOMIZED-PARTITION(A, p, r)
		RANDOMIZED-QUICKSORT(A, p, q - 1)
		RANDOMIZED-QUICKSORT(A, q + 1, r)
```

## 7.4 Analysis of quicksort

### 7.4.1 Worst-case analysis

We saw in Section 7.2 that a worst-case split at every level of recursion in quicksort produces &Theta;(n<sup>2</sup>) running time, which, intuitively, is the worst-case running time of the algorithm.

### 7.4.2 Expected running time

We have already seen the intuition behind why the expected running time of RANDOMIZED-QUICKSORT is O(nlg n): if, in each level of recursion, the split induced by RANDOMIZED-QUICKSORT puts any constant fraction of the elements on one side of the partition, then the recursion tree has depth &Theta;(lg n), and O(n) work is performed at each level.

**Lemma 7.1** Let X be the number of comparisons performed in line 4 of PARTITION over the entire execution of QUICKSORT on an n-element array. Then the running time of QUICKSORT is O(n + X).

Thus we conclude that, using RANDOMIZED-PARTITION, the expected running time of quicksort is O(nlg n) when element values are distinct.

