# Chapter 2. Getting Started

## 2.1 Insertion sort

**Sorting Problem**

- Input: A sequence of n numbers a<sub>1</sub>, a<sub>2</sub>, ... , a<sub>n</sub>.

- Ouput: A permutation (reordering) b<sub>1</sub>, b<sub>2</sub>, ... , b<sub>n</sub> of the input sequence such that 
b<sub>1</sub> <= b<sub>2</sub> <= ... <= b<sub>n</sub>.

```
INSERTION-SORT(A)
	for j = 2 to A.length
		key = A[j]
		// Insert A[j] into the sorted sequence A[1 .. j - 1]
		i = j - 1
		while i > 0 and A[i] > key
			A[i + 1] = A[i]
			i = i - 1
		A[i + 1] = key
```

## 2.2 Analyzing algorithms

- Analyzing an algorithm has come to mean predicting the resources that the algorithm requires.

**Analysis of insertion sort**

- The best case occurs if the array is already sorted. Thus it is a linear function of n.

- If the array is in reverse sorted order, in decreasing order - the worst case result. Thus it is a quadratic function fo n.

**Worst-case and average-case analysis**

- The worst-case running time of an algorithm gives us an upper bound on the running time for any input.

- The "average-case" is often roughly as bad as the worst case.

**Order of growth**

- Consider only the leading term of a formula, since the lower-order terms are relatively insiginificant for large values of n. We also ignore the leading term's constant coefficient.

- We write that insertion sort has a worst-case running time of &theta (n<sub>2<\sub>)

## 2.3 Designing algorithms




