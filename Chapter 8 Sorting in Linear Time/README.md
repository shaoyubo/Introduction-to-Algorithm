# Chapter 8. Sorting in Linear Time

## Chapter 8.1 Lower bounds for sorting

In a comparison sort, we use only comparisons between elements to gain order information about an input sequence a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>. That is, given two elements a<sub>i</sub> and a<sub>j</sub>, we perform one of the tests a<sub>i</sub> < a<sub>j</sub>, a<sub>i</sub> &le; a<sub>j</sub>, a<sub>i</sub> = a<sub>j</sub>, a<sub>i</sub> &ge; a<sub>j</sub> or a<sub>i</sub> > a<sub>j</sub> to determine their relative order. 

In this section, we assume without loss of generality that all the input elements are distinct. Given this assumption, comparisons of the form a<sub>i</sub> = a<sub>j</sub> are uselss, so we can assume that no comparisons of this form are made. We also note that the comparisons a<sub>i</sub> &le; a<sub>j</sub>, a<sub>i</sub> &ge; a<sub>j</sub>, a<sub>i</sub> > a<sub>j</sub>, and a<sub>i</sub> < a<sub>j</sub> are all equivalent in that they yeild identical information about the relative order of a<sub>i</sub> and a<sub>j</sub>. We therefore assume that all comparisons have the form a<sub>i</sub> < a<sub>j</sub>.

**The decision-tree model**

We can view comparison sorts abstractly in terms of decision trees. A decision tree is a full binary tree that represents the comparisons between elements that are performed by a particular sorting algorithm operating on an input of a given size. In a decision tree, we annotate each internal node by i:j for some i and j in the range 1 &le; i, j &le;n, where n is the number of elements in the input sequence. We also annotate each leaf by a permutation &pi;(1), &pi;(2), ..., &pi;(n).