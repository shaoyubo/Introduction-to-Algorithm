# Chapter 11. Hash Tables

Many applications require a dynamic set that supports only the dictonary operations INSERT, SEARCH, AND DELETE. For example, a compiler that translates a programming language maintains a symbol table, in which the keys of elements are arbitrary character strings corresponding to identifiers in the language. A hash table is an effective data structure for implementing dictionaries. Although searching for an element in a hash table can take as long as searching for an element in a linked list - &Theta;(n) time in the worst case - in practice, hashing performs extremely well. Under reasonable assumptions, the average time to search for an element in a hash table is O(1). 

## 11.1 Direct-address tables

Direct addressing is a simple technique that works well when the universe U of keys is reasonably small. Suppose that an application needs a dynamic set in which each element has a key drawn from the universe U = {0, 1, ..., m - 1}, where m is not too large. We shall assume that no two elements have the same key.

To represenet the dynamic set, we use an array, or direct-address table, denoted by T[0 .. m - 1], in which each position, or slot, corresponds to a key in the universe U. Slot k points to an element in the set with key k. If the set contains no element with key k, then T[k] = NIL.

The directory operations are trivial to implement:

```
DIRECT-ADDRESS-SEARCH(T, k)
	return T[k]

DIRECT-ADDRESS-INSERT(T, x)
	T[x.key] = x

DIRECT-ADDRESS-DELETE(T,x)
	T[x.key] = NIL
```

Each of these operation takes only O(1) time.

## 11.2 Hash tables

The downside of direct addressing is obvious: if the universe U is large, storing a table T of size |U| may be impractical, or even impossible, given the memory availalbe on a typical computer. Furthermore, the set K of keys actually stored may be so small relative to U that most of the space allocated for T would be wasted.

When the set K of keys stored in a dictionary is much smaller than the universe U of all possible keys, a hash table requires much less storage than a direct-address table. Specifically, we can reduce the storage requirement to &Theta;(|K|) while we maintain the benefit that searching for an element in the hash table still require O(1) time. The catch is that this bound is for the average-case time, whereas for direct addressing it holds for the worst-case time.

With direct addressing, an element with key k is stored in slot k. With hashing, this element is stored in slot h(k); that is, we use a hash function h to compute the slot from the key k. Here, h maps the universe U of keys into the slots of a hash table T[0 .. m - 1]:

> h: U &arrow; {0, 1, ..., m - 1}