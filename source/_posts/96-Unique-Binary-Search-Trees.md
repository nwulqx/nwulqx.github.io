---
title: 96. Unique Binary Search Trees
date: 2021-10-12 22:43:37
tags:
- LeetCode-medium
- DP(动态规划)
---

Given an integer `n`, return *the number of structurally unique **BST'**s (binary search trees) which has exactly* `n` *nodes of unique values from* `1` *to* `n`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

```
Input: n = 3
Output: 5
```

**Example 2:**

```
Input: n = 1
Output: 1
```

  <!-- more -->

**Constraints:**

- `1 <= n <= 19`

# 分析

dp问题：可<a href ='https://leetcode.com/problems/unique-binary-search-trees/discuss/31666/DP-Solution-in-6-lines-with-explanation.-F(i-n)-G(i-1)-*-G(n-i)'>参考</a>

**javascript**

```javascript
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/unique-binary-search-trees-ii/
 * Runtime: 96 ms, faster than 33.61%
 * Memory Usage: 38.4 MB, less than 74.80% 
 */
/**
 * @param {number} n
 * @return {number}
 */
var numTrees = function(n) {
    const dp = [...Array(22)].map(r => 0);
    dp[0] = dp[1] = 1;
    for(let cnt = 2; cnt <= n; cnt++){
        for(let left = 1; left <= cnt; left++){
            dp[cnt] += dp[cnt-left] * dp[left-1];
        }
    }
    return dp[n];
};
```

**c++**

```c++
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/unique-binary-search-trees-ii/
 * Runtime: 96 ms, faster than 33.61%
 * Memory Usage: 38.4 MB, less than 74.80% 
 */
class Solution {
public:
    int numTrees(int n) {
        int dp[22] = {0};
        dp[0] = dp[1] = 1;
        for(int i = 2; i <= n;i++){
            for(int left = 1; left <= i; left++){
                dp[i] += dp[left - 1] * dp[i - left];
            }
        }
        return dp[n];
    }
};
```

# 总结

dp问题，关键看清楚迭代式~