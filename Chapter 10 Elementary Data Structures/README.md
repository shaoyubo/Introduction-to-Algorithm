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

