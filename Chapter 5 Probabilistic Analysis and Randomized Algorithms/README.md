# Chapter 5. Probabilistic Analysis and Randomized Algorithms

## 5.1 The hiring problem

Suppose that you need to hire a new office assistant. Your previous attempts at hiring have been unsuccessful, and you decide to use an employment agency. The employment agency sends you one candidate each day. You interview that person and then decide either to hire that person or not. You must pay the employment agency a small fee to interview an applicant. To actually hire an applicant is more costly, however, since you must fire your current office assistant and pay a substantial hiring fee to the employment agency. You are committed to having, at all times, the best possible person for the job. Therefore, you decide that, after interviwing each applicant, if that applicant is better qualified than the current office assistant, you will fire the current office assistant and hire the new applicant. you are willing to pay the resuling price of this strategy, but you wish to estimate what that price will be.

The procedure HIRE-ASSISTANT, given below, expresses this strategy for hiring in pseudocode:

```
HIRE-ASSISTANT(n)
	best = 0
	for i = 1 to n
		interview candidate i
		if candidate i is better than candidate best
			best = i
			hire candidate i
``` 

Let n be the number of the total candidate and m be the number of people hired. Assume interviewing has a low cost, say c<sub>i</sub>, whereas hiring is expensive, costing c<sub>h</sub>. Then the total cost associated with the above algorithm is O(c<sub>i</sub>n + c<sub>h</sub>m). No matter how many people we hire, we always interview n candidates and thus always incure the cost c<sub>i</sub>n associated with interviewing. We therefore concentrate on analyzing c<sub>h</sub>m, the hiring cost.

**Worst-case analysis**

In the worst case, we actually hire every candidate that we interview. This situation occurs if the candidates come in strictly increasing order of quality, in which case we hire n times, for a total hiring cost of O(c<sub>h</sub>n).

**Probabilistic analysis**

Probabilistic analysis is the use of probability in the analysis of problems. Most commonly, we use probabilistic analysis to analyze the running time of an algorithm. In order to perform a probabilistic analysis, we must use knowledge of, or make assumptions about, the distribution of the inputs. Then we analyze our algorithm, computing an average-case running time, where we take the average over the distribution of the possible inputs. Thus we are, in effect, averaging the running time over all possible inputs. When reporting such a running time, we will refer to it as the average-case running time.

For the hiring problem, we can assume that the applicants come in a random order. Alternatively, we say that the ranks form a uniform random permutation; that is, each of the possible n! permutations appears with equal probability.

**Randomized algorithms**

We call an algorithm randomized if its behavior is determined not only by its input but also by values produced by a random-number generator. We shall assume that we have at our disposal a random-number generator RANDOM. A call to RANDOM(a, b) returns an integer bewteen a and b, inclusive, with each such integer being equally likely.

When analyzing the running time of a randomized algorithm, we take the expectation of the running time over the distribution of values returned by the random number generator. We distinguish these algorithms from those in which the input is random by referring to the running time of a randomized algorithm as an expected running time.

## 5.2 Indicator random variables



