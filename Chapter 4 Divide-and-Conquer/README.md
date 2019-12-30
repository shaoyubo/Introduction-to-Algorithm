# Chapter 4. Divide-and-Conquer

## 4.1 The maximum-subarray problem

Suppose that you been offered the opportunity to invest in the Volatile Chemical Corporation. Like the checmicals the company produces, the stock price of the Volatile Chemical Corporation is rather volatile. You are allowed to buy one unit of stock only one time and then sell it at a later date, buying and selling after the close of trading for the day. To compensate for this restriction, you are allowed to learn what the price of the stock will be in the future. You goal is to maximize your profit.

**A brute-force solution**

Try every possible pair of buy and sell dates in which the buy date precedes the sell date. A period of n days has n choose 2 such pairs of dates. And the approach would take &Omega;(n<sup>2</sup>) time.

**A solution using divide-and-conquer**

Suppose we want to find a maximum subarray of the subarray A[low .. high]. Divide-and-conquer suggests that we divide the subarray into two subarrays of as equal size as possible. That is, we find the midpoint, say mid, of the subarray, and consider the subarrays A[low .. mid] and A[mid 
+ 1 .. high]. 

The procedure FIND-MAX-CROSS-SUBARRAY (&Theta;(n) time) takes as input the array A and the indices low, mid, and high, and it returns a tuple containing the indices demarcating a maximum subarray that crosses the midpoint, along with the sum of the values in a maximum subarray.

```
FIND-MAX-CROSS-SUBARRAY(A, low, mid, high)
	left-sum = Integer.MIN_VALUE
	sum = 0
	for i = mid downto low
		sum = sum + A[i]
		if sum > left-sum
			left-sum = sum
			max-left = i
	right-sum = Integer.MIN_VALUE
	sum = 0
	for j = mid + 1 to high
		sum = sum + A[j]
		if sum > right-sum
			right-sum = sum
			max-right = j
	return (max-left, max-right, left-sum + right-sum)
```

With a linear-time FIND-MAX-CROSS-SUBARRAY procedure in hand, we can write pseudocode for a divide-and-conquer algorithm to solve the maximum-subarray problem:

```

```






