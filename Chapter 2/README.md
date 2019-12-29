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




