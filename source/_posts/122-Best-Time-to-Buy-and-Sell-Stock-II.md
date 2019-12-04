---
title: 122. Best Time to Buy and Sell Stock II
date: 2017-06-16 17:34:12
tags:
- LeetCode-easy
---
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

<!-- more -->

# Solution
>这道题比较有争议，仔细思考，很简单，只要把赚钱的段取出，相加即可，那这道题这样想的话其实没有可做性了。

```java
public class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length==0){
            return 0;
        }
        int profit = 0;
        for(int i=1;i<prices.length;i++){
            if(prices[i]>prices[i-1]){
                profit += (prices[i]-prices[i-1]);
            }
        }
        return profit;
    }
}
```

# 总结
>这种题目应该是，想起来有问题，而做起来是很简单的问题。我觉得还是应该仔细想想出题人的目的。