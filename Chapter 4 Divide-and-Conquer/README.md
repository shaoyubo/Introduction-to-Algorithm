# Chapter 4. Divide-and-Conquer

## 4.1 The maximum-subarray problem

Suppose that you been offered the opportunity to invest in the Volatile Chemical Corporation. Like the checmicals the company produces, the stock price of the Volatile Chemical Corporation is rather volatile. You are allowed to buy one unit of stock only one time and then sell it at a later date, buying and selling after the close of trading for the day. To compensate for this restriction, you are allowed to learn what the price of the stock will be in the future. You goal is to maximize your profit.

**A brute-force solution**

Try every possible pair of buy and sell dates in which the buy date precedes the sell date. A period of n days has n choose 2 such pairs of dates. And the approach would take &Omega;(n<sub>2</sub>) time.

**A transformation**






