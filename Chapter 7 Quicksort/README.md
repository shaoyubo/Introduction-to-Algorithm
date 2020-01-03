# Chapter 7. Quicksort

The quicksort algorithm has a worst-case running time of &Theta;(n<sup>2</sup>) on an input array of n numbers. Despite this slow worst-case running time, quicksort is often the best practical choice for sorting because it is remarkably efficient on the average: its expected running time is &Theta;(nlg n), and the constant factors hidden in the &Theta;(nlg n) notation are quite small.

## 7.1 Description of quicksort

Quicksort, like merge sort, applies the divide-and-conquer paradigm introduced in Section 2.3.1. Here is the three-step divide-and-conquer process for sorting a typical subarray A[p .. r]:

- Divide: Partition (rearrange) the array A[p .. r] into two (possibly empty) subarrays A[p .. q - 1] and A[q + 1 .. r] such that each element of A[p .. q - 1] is less than or equal to A[q], which is, in turn, less than or equal to each element of A[q + 1 .. r]. Compute the index q as part of this partitioning procedure.

- Conquer: Sort the two subarrays A[p .. q - 1] and A[q + 1 .. r] by recursive calls to quicksort.

- Combine: Because the subarrays are already sorted, no work is needed to combine them: the entire array A[p .. r] is now sorted.

The follwoing procedure implements quicksort:

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



