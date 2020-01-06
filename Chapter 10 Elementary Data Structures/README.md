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

