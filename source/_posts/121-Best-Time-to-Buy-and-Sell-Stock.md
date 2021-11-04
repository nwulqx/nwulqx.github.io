---

title: 121. Best Time to Buy and Sell Stock
date: 2017-06-16 17:19:11
tags:
- LeetCode-easy
- 最长公共子序列（LCS）
- Array
- DP(动态规划)
---
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

**Example 1:**

	Input: [7, 1, 5, 3, 6, 4]
	Output: 5
	max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)

<!-- more -->

**Example 2:**

	Input: [7, 6, 4, 3, 1]
	Output: 0
	In this case, no transaction is done, i.e. max profit = 0.
# Solution

## Brute Force

>使用暴力方法解，怎么想怎么写，双层循环解决。
>LeetCode: Time Limit Exceeded

## Solution1

这道题，为什么会感觉很难做，因为逻辑没有搞清楚：

1. 什么时候卖出？只要当前利益比它最大收益大，就卖出（可惜不是预测。）

什么时候买进？当前值小于上一次买进的值，就应该买进。
2. 什么时候买进？当前值小于上一次买进的值，就应该买进。

总结：买进和卖出没有联系，卖出是买进前的最大利益，所以当输入[7, 6, 8, 3, 1]，虽然买进是1，但是获利最大是8-6=2，利润是2。

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
 * Beats : 90 %;
 */
public class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length==0){
            return 0;
        }
        int profit = 0;
        int buy = prices[0];
        for(int i=1;i<prices.length;i++){
            if(prices[i]-buy>profit){
                profit = prices[i] - buy;
            }else{
                if(prices[i]<buy){
                    buy = prices[i];
                }
            }
        }
        return profit;
    }
}
```

## Solution2
### <a href="https://zh.wikipedia.org/wiki/%E6%9C%80%E9%95%BF%E5%85%AC%E5%85%B1%E5%AD%90%E5%BA%8F%E5%88%97">最长公共子序列</a>

其实这类问题就是动态规划问题，动态规划问题，需要想清楚：

1. 如果设置一个数组，这个数组存储的是动态规划时的什么数据？这个数据决定当前节点，所得到的结果。
2. 结果一定是通过之前创建的动态规划数组得到的。

具体思路：
1. 设置一个数组，用作动态规划数组，这个数组优化后可以不要，但易于理解，脑子里要有他。
2. 这个数组的意义：用于存放当前节点所能获取的最大利润，每次到当前节点都要计算他与买时的差值，如果是正数，则计入动态规划数组；如果是负值，则置为0，此外还应，看看是否比买入低，重置买入值。

**c++实现**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
 * Runtime: 116 ms, faster than 73.65%
 * Memory Usage: 93.3 MB, less than 90.75%
 */
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int res = 0;
        int buy = prices[0];
        for(int i = 1; i < prices.size(); i++){
            buy = min(buy, prices[i]);
            res = max(res, prices[i]-buy);
        }
        return res;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
 * Runtime: 96 ms, faster than 77.95%
 * Memory Usage: 48.7 MB, less than 70.14%
 */
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let buy = prices[0];
    let res = 0;
    for(let i = 1; i < prices.length; i++){
        res = Math.max(prices[i]-buy,res);
        buy = Math.min(buy,prices[i]);
    }
    return res;
};
```



**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
 * Beats : 100%;
 */
public class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length==0){
            return 0;
        }
        int profit = 0;
        int max = 0;
        for(int i=1;i<prices.length;i++){
            profit += (prices[i] - prices[i-1]);
            profit = Math.max(0,profit);
            max = Math.max(max,profit);
        }
        return max;
    }
}
```

**python实现**

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) < 1:
            return 0
        buy = prices[0]
        profit = 0
        for i in range(1,len(prices)):
            if prices[i]-buy>profit:
                profit = prices[i]-buy
            elif prices[i]<buy:
                buy = prices[i]
        return profit
```



# 总结

>这个是比较简单的动态规划问题了，动态规划在于动态规划数组的设置意义，它是用来存储什么意义的值的，这个一定要想清楚。