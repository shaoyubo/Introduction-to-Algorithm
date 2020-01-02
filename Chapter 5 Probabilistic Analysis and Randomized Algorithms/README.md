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

Let n be the number of the total candidate and m be the number of people hired. Assume interviewing has a low cost, say c<sub>i</sub>, whereas hiring is expensive, costing c<sub>h</sub>. Then the total cost associated with the above algorithm is O(c<sub>i</sub>n + c<sub>h</sub>m)
