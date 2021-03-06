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

In order to analyze many alogrithms, including the hiring problem, we use indicator random variables. Indicator random variables provide a convenient method for converting betwee probabilities and expectations. Suppose we are given a sample space S and an event A. Then the indicator random variable I{A} associated with event A is defined as I{A} = 1 if A occurs, I{A} = 0 if A does not occur.

**Lemma 5.1**

Given a sample space S and an event A in the sample space S, ket X<sub>A</sub> = I{A}. Then E[X<sub>A</sub>] = Pr{A}.

**Analysis of the hiring problem using indicator random variables**

**Lemma 5.2**

Assumming that the candidates are presented in a random order, algorithm HIRE-ASSISTANT has an average-case total hiring cost of O(c<sub>h</sub>ln n).

## 5.3 Randomized algorithms

For the hiring problem, the only change needed in the code is to randomly permute the array.

```
RANDOMIZED-HIRE-ASSISTANT(n)
	randomly permute the list of candidates
	best = 0
	for i = 1 to n
		interview candidate i
		if candidade i is better than candidate best
			best = i
			hire candidate i
```

With this simple change, we have created a randomized algorithm whose performance matches that obtained by assuming that the candidates were presented in a random order.

**Lemma 5.3**

The expected hiring cost of the procedure RANDOMIZED-HIRE-ASSISTANT is O(c<sub>h</sub>ln n).

**Randomly permuting arrays**

Many randomized algorithms randomize the input by permuting the given input array. Our goal is to produce a random permutation of the array. We use a range of 1 to n<sup>3</sup> to make it likely that all the priorities in P are unique.

```
PERMUTE-BY-SORTING(A)
	n = A.length
	let P[1 .. n] be a new array
	for i = 1 to n
		P[i] = RANDOM(1, n^3)
	sort A, using P as sort keys
```

**Lemma 5.4**

Procedure PERMUTE-BY-SORTING produces a uniform random permutation of the input, assuming that all priorities are distinct.

A better method for generating a random permutation is to permute the given array in place. The procedure RANDOMIZED-IN-PLACE does so in O(n) time.

```
RANDOMIZED-IN-PLACE(A)
	n = A.length
	for i = 1 to n
		swap A[i] with A[RANDOM(i, n)]
```

**Lemma 5.5**

Procedure RANDOMIZED-IN-PLACE computes a uniform random permutation.

## 5.4 Probabilistic analysis and further uses of indicator random variables

### 5.4.1 The birthday paradox

Our first example is the birthday paradox. How many people must there be in a room before there is a 50% chance that two of them were born on the same day of the year? To answer this question, we index the people in the room with the integers 1, 2, ..., k, where k is the number of people in the room. We ignore the issue of leap years and assume that all years have n = 365 days. For i = 1, 2, ..., k, let b<sub>i</sub> be the day of the year on which person i's birthday falls, where 1 &le; b<sub>i</sub> &le; n. We also assume that birthdays are uniformly distributed across the n days of the year, so that Pr{b<sub>i</sub> = r} = 1/n for i = 1, 2, ..., k and r = 1, 2, ..., n.

The probability that two given people, say i and j, have matching birthdays depends on whether the random selection of birthdays is independent. We assume from now on that birthdays are independent, so that the probability that i's birthday and j's birthday both fall on day r is Pr{b<sub>i</sub> = r and b<sub>j</sub> = r} = Pr{b<sub>i</sub>}Pr{b<sub>j</sub> = 1/n<sup>2</sup>. Thus, the probability that they both fall on the same day is Pr{b<sub>i</sub> = b<sub>j</sub>} = 1/n. More intuitively, once b<sub>i</sub> is chosen, the probability that b<sub>j</sub> is chosen to be the same day is 1/n.

For n = 365, we must have at least 23 days people are in a room, the probability is at least 1/2 that at least two people have the same birthday.

**An analysis using indicator random variables**

We can use indicator random variables to provide a simpler but approximate analysis of the birthday paradox. For each pair (i, j) of the k people in the room, we define the indicator random variable X<sub>ij</sub>, for 1 &le; i < j &le; k, by X<sub>ij</sub> = 1 if person i and person j have the same birthday, 0 otherwise. Then E[X<sub>ij</sub>] = Pr{person i and person j have the same birthday} = 1/n. Letting X be the random variable that counts the number of pairs of individuals having the same birthday, we have 

> X = &sum;<sub>i = 1</sub><sup>k</sup>&sum;<sub>j = i + 1</sub><sup>k</sup> X<sub>ij</sub>. 

Then E[X] = k(k-1)/2n. 

For the above two analysis, the yare the same asymptotically: &Theta;(n<sup>1/2</sup>).

### 5.4.2 Balls and bins

Consider a process in which we randomly toss identical balls into b bins, numbered 1, 2, ..., b. The tosses are independent, and on each toss the ball is equally likely to end up in any bin. The probability that a tossed ball lands in any given bin is 1/b. Thus, the ball-tossing process is a sequence of Bernoulli trials with a probability 1/b of success, where success means that the ball falls in the given bin. This model is particularly useful for analyzing hasing and we can answer a variety of interesting questions about the ball-tossing process.

**How many balls fall in a given bin?**
The number of balls that fall in a given bin follows the binomial distribution b(k;n, 1/b). If we toss n balls, the expected number of balls that fall in the given bin is n/b.

**How many balls must we toss, on the average, until a given bin contains a ball?** 
The number of tosses until the given bin receives a ball follows the geometric distribution with probability 1/b and the expected number of tosses until success is b.

**How many balls must we toss until every bin contains at least one ball?**
Let us call a toss in which a ball falls into an empty bin a "hit". We want to know the expected number n of tosses required to get b hits. Thus for each toss in the ith stage, the probability of obtaining a hit is (b - i + 1)/b. Let n<sub>i</sub> denote the number of tosses in the ith stage. Thus, the number of tosses required to get b hits is n = &sum;<sub>i = 1</sub><sup>b</sup> n<sub>i</sub>. Each random variable n<sub>i</sub> has a geometric distribution with probability of success (b - i + 1)/b and thus, we have E[n] = b(ln b + O(1)).

### 5.4.3 Streaks

Suppose you flip a fair coin n times. What is the longest streak of consecutive heads that you expect to see? The answer is &Theta;(lg n).

### 5.4.4 The online hiring problem

As a final example, we consider a variant of the hiring problem. Suppose now that we do not wish to interview all the candidates in order to find the best one. We also do not wish to hire and fire as we find better and better applicants. Instead, we are willing to settle for a candidate who is close to the best, in exchange for hiring exactly once. We must obey one company requirement: after each interviw we must either immediately offer the position to the applicant or immediately reject the applicant. What is the trade-off between minimizing the amount of the interviewing and maximizing the quality of the candidate hired.

We can model this problem in the following ways. After meeting an applicant, we are able to give each one a score; let score(i) denote the score we give to the ith applicant, and assume that no two applicants receive the same score. After we have seen j applicants, we know which of the j has the highest score, but we do not know whether any of the remaining n - j applicants will receive a higher score. We decide to adopt the strategy of selecting a positiv integer k < n, interviewing and then rejecting the first k applicants, and hiring the first applicant thereafter who has a higher score than all preceding applicants. If it turns out that the best-qualified applicant was among the first k interviewed, then we hire the nth applicant. We formalize this strategy in the procedure ON-LINE-MAXIMUM(k,n), which return the index of the candidate we wish to hire.

```
ON-LINE-MAXIMUM(k, n)
	bestscore = Integer.MIN_VALUE
	for i = 1 to k
		if score(i) > bestscore
			bestscore = score(i)
	for i = k + 1 to n
		if score(i) > bestscore
			return i
	return n
```

