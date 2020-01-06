# Chapter 10. Elementary Data Structures

## 10.1 Stacks and queues

Stacks and queues are dynamic sets in which the element removed from the set by the DELETE operation is prespecified. In a stack, the element deleted from the set is the one most recently inserted: the stack implements a last-in, first-out, or LIFO, policy. Similarly, in a queue, the element deleted is always the one that has been in the set for the longest time: the queue implements a first-in, first-out, or FIFO, policy.

**Stacks**

The INSERT operation on a stack is often called PUSH, and the DELETE opertaion, which dose not take an element argument, is often called POP. We can implement a stack of at most n elements with an array S[1 .. n]. The array has an attribute S.top that indexes the most recently inserted element. The stack consists of elements S[1 .. S.top], where S[1] is the element at the bottom of the stack and S[S.top] is the element at the top.

When S.top = 0, the stack contains no elements and is empty. We can test to see whether the stack is empty by query operation STACK-EMPTY. If we attempt to pop an empty stack, we say the stack underflows, which is normally an error. If S.top exceeds n, the stack overflows.

We can implement each of the stack operations with just a few lines of code:

```
STACK-EMPTY(S)
	if S.top == 0
		return TRUE
	else
		return FALSE

PUSH(S, x)
	S.top = S.top + 1
	S[S.top] = x

POP(S)
	if STACK-EMPTY(S)
		error "underflow"
	else
		S.top = S.top - 1
		return S[S.top + 1]
```

Each of the above three stack operations takes O(1) time.

**Queues**

We call the INSERT operation on a queue ENQUEUE, and we call the DELETE operation DEQUEUE. The FIFO property of a queue causes it to operate like a line of customers waiting to pay a cashier. The queue has a head and a tail. When an element is enqueued, it takes its place at the tail of the queue, just as a newly arriving customer takes a place at the end of the line. The element dequeued is always the one at the head of the queue, like the customer at the head of the line who has waited the longest.

The queue has an attribute Q.head that indexes, or points to, its head. If we attempt to dequeue an element from an empty queue, the queue underflows. When Q.head = Q.tail + 1, the queue is full, and if we attempt to enqueue an element, then the queue overflows.

```
ENQUEUE(Q, x)
	Q[Q.tail] = x
	if Q.tail == Q.length
		Q.tail = 1
	else
		Q.tail = Q.tail + 1

DEQUEUE(Q)
	x = Q[Q.head]
	if Q.head == Q.length
		Q.head = 1
	else
		Q.head = Q.head + 1
	return x
```

Each operation takes O(1) time.

## 10.2 Linked lists

A linked list is a data structure in which the objects are arranged in a linear order. Unlike an array, however, in which the linear order is determined by the array indices, the order in a linked list is determined by a pointer in each object.

Each element of a doubly linked list L is an object with an attribute key and two other pointer attributes: next and prev. The object may also contain other satellite data. Given an element x in the list, x.next points to its successor in the linked list, and x.prev points to its predecessor. If x.prev = NIL, the element has no predecessor and is therefore the first element, or head, of the list. If x.next = NIL, the element x has no successor and is therefore the last element, or tail, of the list. And attribute L.head points to the first element of the list. If L.head = NIL, the list is empty.

In the remainder of this section, we assume that the lists with which we are working are unsorted and doubly linked.

**Searching a linked list**

The procedure LIST-SEARCH(L, k) finds the first element with key k in list L by a simple linear search, returning a pointer to this element. If no object with key k appears in the list, then the procedure returns NIL.

```
LIST-SEARCH(L, k)
	x = L.head
	while x != NIL and x.key != k
		x = x.next
	return x
```

To search a list of n objects, the LIST-SEARCH procedure takes &Theta;(n) time in the worst case, since it may have to search the entire list.

**Inserting into a linked list**

Given an element x whose key attribute has already been set, the LIST-INSERT procedure "splices" x onto the front of the linked list.

```
LIST-INSERT(L, x)
	x.next = L.head
	if L.head != NIL
		L.head.prev = x
	L.head = x
	x.prev = NIL
```

The running time for LIST-INSERT on a list of n elements is O(1).

**Deleting from a linked list**

The procedure LIST-DELETE removes an element x from a linked list L.

```
LIST-DELETE(L, x)
	if x.prev != NIL
		x.prev.next = x.next
	else 
		L.head = x.next
	if x.next != NIL
		x.next.prev = x.prev
```

LIST-DELETE runs in O(1) time, but if we wish to delete an element with a given key, &Theta;(n) time is required in the worst case because we must first call LIST-SEARCH to find the element.

**Sentinels**

The code for LIST-DELETE would be simpler if we could ignore the boundary conditions at the head and tail of the list:

```
LIST-DELETE'(L, x)
	x.prev.next = x.next
	x.next.prev = x.prev
```

A sentinel is a dummy object that allows us to simplify boundary conditions. We can turn a regular doubly linked list into a circular, doubly linked list with a sentinel, in which the sentinel L.nil lies between the head and tail.

```
LIST-SEARCH'(L, k)
	x = L.nil.next
	while x != L.nil and x.key != k
		x = x.next
	return x

LIST-INSERT'(L, x)
	x.next = L.nil.next
	L.nil.next.prev = x
	L.nil.next = x
	x.prev = L.nil
```

## 10.3 Implementing pointers and objects

**A multiple-array representation of objects**

We can represent a collection of objects that have the same attributes by using an array for each attribute. As an example, we can implement the linked list with three arrays. The array key holds the values of the keys currently in the dynamic set, and the pointers reside in the arrays next and prev. For a given array index x, the array entries key[x], next[x], and prev[x] represent an object in the linked list. Under this interpretation, a pointer x is simply a common index into the key, next, and prev arrays.

**A single-array representation of objects**

The words in a computer memeory are typically addressed by integers from 0 to M - 1, where M is a suitably large integer. In many programming languages, an objet occupies a contiguous set of locations in the computer memory. A pointer is simply the address of the first memory location of the object, and we can address other memory locations within the object by adding an offset to the pointer.

We can use the same strategy for implementing objects in programming environments that do not provide explicit pointer data types.

**Allocating and freeing objects**

To insert a key into a dynamic set represented by a doubly linked list, we must allocate a pointer to a currently unused objet in the linked-list representation. Thus, it is useful to manage the storage of objects not currenty used in the linked-list representation so that one can be allocated. In some systems, a garbage collector is responsible for determining which objects are unused.

Suppose that the arrays in the multiple-array representation have length m and that at some moment the dynamic set contains n &le; m elements. Then n objects represent elements currently in the dynamic set, and the remaining m - n objets are free; the free objects are available to represent elements inserted into the dynamic set in the future.

```
ALLOCATE-OBJECT()
	if free == NIL
		error "out of space"
	else
		x = free
		free = x.next
		return x

FREE-OBJECT(x)
	x.next = free
	free = x
```

The two procedures run in O(1) time, which makes them quiet practical.

## 10.4 Representing rooted trees

We represent each node of a tree by an object. As with linked lists, we assume that each node contains a key attribute. The remaining attributes of interest are points to other nodes, and they vary according to the type of tree.

**Binary trees**

We use the attributes p, left, and right to store pointers to the parent, left child, and right child of each node in a binary tree T. If x.p = NIL, then x is the root. If node x has no left child, then x.left = NIL, and similarly for the right child. The root of the entire tree T is pointed to by the attribute T.root. If T.root = NIL, then the tree is empty.

**Rooted trees with unbounded branching**

We can extend the scheme for representing a binary tree to any class of trees in which the number of children of each node is at most constant k: we replace the left and right attributes by child<sub>1</sub>, child<sub>2</sub>, ... , child<sub>k</sub>. This scheme no longer works when the number of children of a node is unbounded, since we do not know how many attributes to allocate in advance. Moreover, even if the number of children k is bounded by a large constant but most ndes have a small number of children, we may waste a lot of memory.

Fortunately, there is a clever scheme to represent trees with arbitrary numbes of children. It has the advantage of using only O(n) space for any n-node rooted tree. The left-child, right-sibling representation appears. As before, each node contains a parent pointer p, and T.root points to the root of tree T. Instead of having a pointer to each of its children, however, each node x has only two pointers:

1. x.left-child points to the leftmost child of node x, and 

2. x.right-sibling points to the sibling of x immediately to its right.

If node x has no children, then x.left-children = NIL, and if node x is the rightmost child of its parent, then x.right-sibling = NIL.

**Other tree representation**

We sometimes represent rooted trees in other ways. In Chapter 6, for example, we represented a heap, which is based on a complete binary tree, by a single array plus the indesx of the last node in the heap. The trees that appear in Chapter 21 are traversed only toward the root, and so only the parent pointers are present; there are no pointers to children.


