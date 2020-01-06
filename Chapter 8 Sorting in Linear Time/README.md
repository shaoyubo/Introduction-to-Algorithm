# Chapter 8. Sorting in Linear Time

## 8.1 Lower bounds for sorting

In a comparison sort, we use only comparisons between elements to gain order information about an input sequence a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>. That is, given two elements a<sub>i</sub> and a<sub>j</sub>, we perform one of the tests a<sub>i</sub> < a<sub>j</sub>, a<sub>i</sub> &le; a<sub>j</sub>, a<sub>i</sub> = a<sub>j</sub>, a<sub>i</sub> &ge; a<sub>j</sub> or a<sub>i</sub> > a<sub>j</sub> to determine their relative order. 

In this section, we assume without loss of generality that all the input elements are distinct. Given this assumption, comparisons of the form a<sub>i</sub> = a<sub>j</sub> are uselss, so we can assume that no comparisons of this form are made. We also note that the comparisons a<sub>i</sub> &le; a<sub>j</sub>, a<sub>i</sub> &ge; a<sub>j</sub>, a<sub>i</sub> > a<sub>j</sub>, and a<sub>i</sub> < a<sub>j</sub> are all equivalent in that they yeild identical information about the relative order of a<sub>i</sub> and a<sub>j</sub>. We therefore assume that all comparisons have the form a<sub>i</sub> < a<sub>j</sub>.

**The decision-tree model**

We can view comparison sorts abstractly in terms of decision trees. A decision tree is a full binary tree that represents the comparisons between elements that are performed by a particular sorting algorithm operating on an input of a given size. In a decision tree, we annotate each internal node by i:j for some i and j in the range 1 &le; i, j &le;n, where n is the number of elements in the input sequence. We also annotate each leaf by a permutation &pi;(1), &pi;(2), ..., &pi;(n). The execution of the sorting algorithm corresponds to tracing a simple path from the root of the decision tree down to a leaf. Each internal node indicates a comparison a<sub>i</sub> &le; a<sub>j</sub>. The left subtree then dictates a subsequent comparisons once we know that a<sub>i</sub> &le; a<sub>j</sub>, and the right subtree dictates subsequent comparisons knowing that a<sub>i</sub> > a<sub>j</sub>. When we come to a leaf, the sorting algorithm has established the ordering a<sub>&pi;(1)</sub> &le; a<sub>&pi;(2)</sub> &le; ... &le; a<sub>&pi;(n)</sub>. Because any correct sorting algorithm must be able to produce each permutation of its input, each of the n! permutations on n elements must appear as one of the leaves of the decision tree for a comparison sort to be correct. Furthermore, each of these leaves must be reachable from the root by a downward path corresponding to an actual execution of the comparison sort. Thus, we shall consider only decision trees in which each permutation appears as a reachable leaf.

**A lower bound for the worst case**

The worst case number of comparisons for a given comparison sort algorithm equals the height of its decision tree. A lower bound on the heights of all decision trees in which each permutation appears as a reachable leaf is therefore a lower bound on the running time of any comparison sort algorithm. The following theorem establishes such a lower bound.

**Theorem 8.1** 

> Any comparison sort algorithm requires &Omega;(nlg n) comparisons in the worst case.

**Corollary 8.2**

> Heapsort and merge sort are asymptotically optimal comparison sorts.


## 8.2 Counting sort

Counting sort assumes that each of the n input elements is an integer in the range 0 to k, for some integer k. When k = O(n), the sort runs in &Theta;(n) time. Counting sort determines, for each input element x, the number of elements less than x. It uses this information to place element x directly into its position in the output array.  

In the code for counting sort, we assume that the input is an array A[1 .. n], and thus A.length = n. We require two other arrays: the array B[1 .. n] holds the sorted output, and the array C[0 .. k] provides temporary working storage.

```
COUNTING-SORT(A, B, k)
	let C[0 .. k] be a new array
	for i = 0 to k
		C[i] = 0
	for j = 1 to A.length
		C[A[j]] = C[A[j]] + 1 
	// C[i] now contains the number of elements equal to i.
	for i = 1 to k
		C[i] = C[i] + C[i - 1]
	// C[i] now contains the number of elements less than or equal to i
	for j = A.length downto 1
		B[C[A[j]]] = A[j]
		C[A[j]] = C[A[j]] - 1
```

The overall time is &Theta;(k + n). In practice, we usually use counting sort when we have k = &Theta;(n), in which case the running time is &Theta;(n).

Counting sort beats the lower bound of &Omega;(nlg n) because it is not a comparison sort. And an important property of counting sort is that it is stable: numbers with the same value appear in the output array in the same order as they do in the input array. Counting sort's stability is important for another reason: counting sort is oftern used as a subroutine in radix sort.

## 8.3 Radix sort

Radix sort is the algorithm used by the card-sorting machines you now find only in computer museums. The cards have 80 columns, and in each column a machine can punch a hole in one of 12 places. The sorter can be mechanically "programmed" to examine a given column of each card in a deck and distribute the card into one of 12 bins depending on which place has been punched. An operator can then gather the cards bin by bin, so that cards with the first place punched are on top of cards with the second place punched, and so on.

Radix sort solves the problem of card sorting - counterintuitively - by sorting on the least significant digit first. In order for radix sort to work correctly, the digit sorts must be stable. The sort performed by a card sorter is stable, but the operator has to be wary about not changing the order of the cards as they come out of a bin, even though all the cards in a bin have the same digit in the chosen column.

```
RADIX-SORT(A, d)
	for i = 1 to d
		use a stable sort to sort array A on digit i
```

**Lemma 8.3**

> Given n d-digit numbers in which each digit can take on up to k possible values, RADIX-SORT correctly sorts these numbers in &Theta;(d(n + k)) time if the stable sort it uses takes &Theta;(n + k) time.

**Lemma 8.4**

> Given n b-bit numbers and any positive integer r &le; b, RADIX-SORT correctly sorts these numbers in &Theta;((b/r)(n + 2<sup>r</sup>)) time if the stable sort it uses take &Theta;(n + k) time for inputs in the range 0 to k.