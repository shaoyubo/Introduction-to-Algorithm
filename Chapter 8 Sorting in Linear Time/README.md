# Chapter 8. Sorting in Linear Time

## Chapter 8.1 Lower bounds for sorting

In a comparison sort, we use only comparisons between elements to gain order information about an input sequence a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>. That is, given two elements a<sub>i</sub> and a<sub>j</sub>, we perform one of the tests a<sub>i</sub> < a<sub>j</sub>, a<sub>i</sub> &le; a<sub>j</sub>, a<sub>i</sub> = a<sub>j</sub>, a<sub>i</sub> &ge; a<sub>j</sub> or a<sub>i</sub> > a<sub>j</sub> to determine their relative order. 

In this section, we assume without loss of generality that all the input elements are distinct. Given this assumption, comparisons of the form a<sub>i</sub> = a<sub>j</sub> are uselss, so we can assume that no comparisons of this form are made. We also note that the comparisons a<sub>i</sub> &le; a<sub>j</sub>, a<sub>i</sub> &ge; a<sub>j</sub>, a<sub>i</sub> > a<sub>j</sub>, and a<sub>i</sub> < a<sub>j</sub> are all equivalent in that they yeild identical information about the relative order of a<sub>i</sub> and a<sub>j</sub>. We therefore assume that all comparisons have the form a<sub>i</sub> < a<sub>j</sub>.

**The decision-tree model**

