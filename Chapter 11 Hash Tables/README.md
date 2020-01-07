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

> h: U &rarr; {0, 1, ..., m - 1}

where the size m of the hash table is typically much less than |U|. We say that an element with key k hashes to slot h(k); we also say that h(k) is the hash value of key k. Instead of a size of |U|, the array can have size m.

There is one hitch: two keys may hash to the same slot. We call this situation a collision. Fortunately, we have effective techniques for resolving the conflict created by collisions.

The ideal solution would be to avoid collisions altogether. We might try to achieve this goal by choosing a suitable hash function h. One idea is to make h appear to be "random", thus avoiding collisions or at least minimizing their number. Thus, while a well-designed, "random"-looking hash function can minimize the number of collisions, we still need a method for resolving the collisions that do occur.

**Collision resolution by chaining**

In chaining, we place all the elements that hash to the same slot into the same linked list. The dictionary operations on a hash table T are easy to implement when collisions are resolved by chaining:

```
CHAINED-HASH-INSERT(T, x)
	insert x at the head of list T[h(x.key)]

CHAINED-HASH-SEARCH(T, k)
	search for an element with key k in list T[h(k)]

CHAINED-HASH-DELETE(T, x)
	delete x from the list T[h(x.key)]
```

The worst-case running time for insertion is O(1). We can delete an element in O(1) time if the lists are doubly linked.

**Analysis of hashing with chaining**

How well does hashing with chaining perform. Given a hash table T with m slots that stores n elements, we define the load factore &alpha; for T as n/m, that is, the average number of elements stored in a chain. The worst-case time for searching is thus &Theta;(n) plus the time to computer the hash function - no better than if we used one linked list for all the elements. 

**Theorem 11.1** 

> In a hash table in which collisions are resolved by chaining, an unsuccessful search takes average-case time &Theta(1 + &alpha;);, under the assumption of simple uniform hashing.

**Theorem 11.2**

> In a hash table in which collisions are resolved by chaining, a successful search takes average-case time &Theta(1 + &alpha;);, under the assumption of simple uniform hashing.

What does this analysis mean? If the number of hash-table slots is at least proportional to the number of elements in the table, we have n = O(m) and, consequently, &alpha; = n/m = O(m)/m = O(1). Thus, searching takes constant time on average. Since insertion O(1) worst-case time and deletion takes O(1) worst-case time when the lists are doubly linked, we can support all dictionary operations in O(1) time on average.