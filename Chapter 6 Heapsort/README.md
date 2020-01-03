# Chapter 6. Heapsort

In this chapter, we introduce another sorting algorithm: heapsort. Like merge sort, but unlike insertion sort, heapsort's running time is O(nlg n). Like insertion sort, but unlike merge sort, heapsort sorts in place: only a constant number of array element are stored outside the input array at any time. Thus, heapsort combines the better attributes of the two sorting algorithms we have already discussed.

## 6.1 Heaps

The (binary) heap data structure is an array object that we can view as a nearly complete binary tree. Each node of the tree corresponds to an element of the array. The tree is completely filled on all levels except possibly the lowest, which is filled from the left up to a point. An array A that represnets a heap is an object with two attributes: A.length, which gives the number of elements in the array and A.heap-size, which represents how many elements in the heap are stored within array A. That is although A[1 .. A.length] may contain numbers, only the elements in A[1 .. A.heap-size], where 0 &le; A.heap-size &le; A.length, are valid elements of the heap. The root of the tree is A[1], and given the index i of a node, we can easily compute the indices of its parent, left child and right child.

```
PARENT(i)
	return Math.floor(i/2)

LEFT(i)
	return 2i

RIGHT(i)
	return 2i + 1
```

There are two kinds of binary heaps: max-heaps and min-heaps. In both kinds, the values in the nodes satisfy a heap propoty, the specifies of which depend on the kind of heap. In a max-heap, the max-heap property is that for every node i other than the root A[PARENT(i)] &ge; A[i], that is, the value of a node is at most the value of its parent. A min-heap is organized in the opposite way; the min-heap property is that for every node i otehr than the root A[PARENT(i)] &le; A[i]. The smallest element in a min-heap is at the root.

For the heapsort algorithm, we use max-heaps. Viewing a heap as a tree, we define the height of a node in a heap to be the number of edges on the longest simple downward path from the node to a leaf, and we define the height of the heap to be the height of its root. Since a heap of n elements is based on a complete binary tree, its height is &Theta;(lg n).

The remaining of this chapter presents some basic procedures and shows how they are used in a sorting algorithm and a priority-queue data structure.

- The MAX-HEAPIFY procedure, which runs in O(lg n) time, is the key to maintaining the max-heap property.

- The BUILD-MAX-HEAP procedure, which runs in linear time, produces a max-heap from an unordered input array.

- The HEAPSORT procedure, which runs in O(nlg n) time, sorts an array in place.

- The MAX-HEAP-INSERT, HEAP-EXTRACT-MAX, HEAP-INCREASE-KEY, and HEAP-MAXMIMUM procedures, which run in O(lg n) time, allow the heap data structure to implement a priority queue.

## 6.2 Maintaining the heap property

In order to maintain the max-heap property, we call the procedure MAX-HEAPIFY. Its inputs are an array A and an index i into the array. When it is called, MAX-HEAPIFY assumes that the binary trees rooted at LEFT(i) and RIGHT(i) are max-heaps, but that A[i] might be smaller than its childern, thus violating the max-heap property.

```
MAX-HEAPIFY(A, i)
	l = LEFT(i)
	r = RIGHT(i)
	if l <= A.heap-size and A[l] > A[i]
		largest = l
	else 
		largest = i
	if r <= A.heap-size amd A[r] > A[largest]
		largest = r
	if largest != i
		exchange A[i] with A[largest]
		MAX-HEAPIFY(A, largest)
```

The running time of MAX-HEAPIFY on a subtree of size n rooted at a given node i is the &Theta;(1) time to fix up the relationships among the elements A[i], A[LEFT(i)], A[RIGHT(i)], plus the time to run MAX-HEAPIFY on a subtree rooted at one of the children of node i. And the running time is T(n) = O(lg n). Alternatively, we can characterize the running time of MAX-HEAPIFY on a node of height h is O(h).

## 6.3 Building a heap

We can use the procedure MAX-HEAPIFY in a bottom-up manner to convert an array A[1 .. n], where n = A.length, into a max-heap. The procedure BUILD-MAX-HEAP goes through the remaining nodes of the tree and runs MAX-HEAPIFY on each one.

```
BUILD-MAX-HEAP(A)
	A.heap-size = A.length
	for i = Math.floor(A.length/2) downto 1
		MAX-HEAPIFY(A, i)
```

We can compute a simple upper bound on the running time of BUILD-MAX-HEAP as follows. Each call to MAX-HEAPIFY costs O(lg n) time, and BUILD-MAX-HEAP makes O(n) such calls. Thus, the running time is O(nlg n). This upper bound, though correct, is not asymptotically tight. Actually, we can build a max-heap from an unordered array in linear time.

## 6.4 The heapsort algorithm

The heapsort algorithm starts by using BUILD-MAX-HEAP to build a max-heap on the input array A[1 .. n], where n = A.length.

```
HEAPSORT(A)
	BUILD-MAX-HEAP(A)
	for i = A.length downto 2
		exchange A[1] with A[i]
		A.heap-size = A.heap-size - 1
		MAX-HEAPIFY(A, 1)
```

The HEAPSORT procedure takes time O(nlg n), since the call to BUILD-MAX-HEAP takes O(n) and each of the n - 1 calls to MAX-HEAPIFY takes time O(lg n).
