---
title: 122. Best Time to Buy and Sell Stock II
date: 2017-06-16 17:34:12
tags:
- LeetCode-easy
- Array
- 贪心(Greedy)
---
Say you have an array `prices` for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example 1:**

```java
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

<!-- more -->

**Example 2:**

```java
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

**Example 3:**

```java
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

 

**Constraints:**

- `1 <= prices.length <= 3 * 10 ^ 4`
- `0 <= prices[i] <= 10 ^ 4`



# 分析
详见：https://leetcode.com/articles/best-time-to-buy-and-sell-stock-ii/

这个题目其实有难度的，虽然直接利用贪心，可以很快的得到答案，但是这么做不是真的解决问题。
我看了答案，提供了三种解法：

## 解法一（暴力法）-Time Limit Exceeded超时

第一种是暴力解法，思路很实际，但是在数据较多的情况下，一定会超时，因为他本身利用了递归。

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii
 * Error:Time Limit Exceeded
 * Beats : 0 %;
 */
class Solution {
    public int maxProfit(int[] prices) {
        return calculate(prices, 0);
    }

    public int calculate(int prices[], int s) {
        if (s >= prices.length)
            return 0;
        int max = 0;
        for (int start = s; start < prices.length; start++) {
            int maxprofit = 0;
            for (int i = start + 1; i < prices.length; i++) {
                if (prices[start] < prices[i]) {
                    int profit = calculate(prices, i + 1) + prices[i] - prices[start];
                    if (profit > maxprofit)
                        maxprofit = profit;
                }
            }
            if (maxprofit > max)
                max = maxprofit;
        }
        return max;
    }
}
```

这个思路用了递归，相当于枚举了所有的情况，进而得出强行得出结果，优点是直接，但缺点也很明显，那就是效率很低。

## 解法二-谷峰法

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii
 * Beats : 93.55%;
 */
class Solution {
    public int maxProfit(int[] prices) {
        int i = 0;
        int valley = prices[0];
        int peak = prices[0];
        int maxprofit = 0;
        while (i < prices.length - 1) {
            while (i < prices.length - 1 && prices[i] >= prices[i + 1])
                i++;
            valley = prices[i];
            while (i < prices.length - 1 && prices[i] <= prices[i + 1])
                i++;
            peak = prices[i];
            maxprofit += peak - valley;
        }
        return maxprofit;
    }
}
```

谷峰法的关键点在于：

>In case we skip one of the peaks (trying to obtain more profit), we will end up losing the profit over one of the transactions leading to an overall lesser profit.
>如果我们跳过其中一个峰值(试图获得更多的利润)，我们最终将失去其中一个交易的利润，导致整体利润减少。



## 解法三-贪心（推荐）

这个贪心其实是在上面谷峰法的基础上改进的，因为谷峰法是把每一段增长段都不能丢弃的全部计算到一起；而贪心则是这些增长段分割为最小段计算总和，虽然题目是不允许同日买进卖出，但其实我们只是在数学意义上进行转换，而不涉及实际操作。

**c++**

```java
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/
 * Runtime: 4 ms, faster than 90.92%
 * Memory Usage: 13.1 MB, less than 46.92%
 */
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int res = 0;
        int buy = prices[0];
        for(int i = 1; i < prices.size(); i++){
            res += max(prices[i]-prices[i-1],0);
        }
        return res;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/
 * Runtime: 80 ms, faster than 61.41%
 * Memory Usage: 40.4 MB, less than 37.96% 
 */
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let res = 0;
    for(let i = 1; i < prices.length; i++){
        res += Math.max(prices[i]-prices[i-1], 0);
    }
    return res;
};
```



# 总结

这个题目关键是谷峰法，而贪心只是谷峰法的一个变化。