---
title: 354. Russian Doll Envelopes
date: 2021-03-07 17:27:47
tags:
- DP(动态规划)
- LIS(最长上升子序列)
---

You are given a 2D array of integers envelopes where envelopes[i] = [wi, hi] represents the width and the height of an envelope.

One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

Return the maximum number of envelopes can you Russian doll (i.e., put one inside the other).

Note: You cannot rotate an envelope.

 <!--more-->

**Example 1:**

> Input: envelopes = [[5,4],[6,4],[6,7],[2,3]]
> Output: 3
> Explanation: The maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).

**Example 2:**

> Input: envelopes = [[1,1],[1,1],[1,1]]
> Output: 1

**Constraints:**

- 1 <= envelopes.length <= 5000
- envelopes[i].length == 2
- 1 <= wi, hi <= 104

# Solution

常规动态规划解法：

```c++
class Solution {
public:
    int maxEnvelopes(vector<vector<int>>& envelopes) {
        sort(envelopes.begin(),envelopes.end());
        int length = envelopes.size();
        vector<int> dp(length,1);
        int result = 1;
        for(int i = 1; i < length; i++){
            for(int j = 0;j < i; j++){
                if(envelopes[j][0]<envelopes[i][0] && envelopes[j][1]<envelopes[i][1]){
                    dp[i] = max(dp[i],dp[j]+1);
                }
            }
            result = max(result,dp[i]);
        }
        return result;
    }
};
```



## 优化方法

常规方法最重要的一点是基于排序的方法，但是排序是有优化点的。

```c++
class Solution {
public:
    int maxEnvelopes(vector<vector<int>>& envelopes) {
        // 排序的重点！
        sort(envelopes.begin(), envelopes.end(), [](const auto& e1, const auto& e2) {
            return e1[0] < e2[0] || (e1[0] == e2[0] && e1[1] > e2[1]);
        });
        int length = envelopes.size();
        vector<int> dp(length,1);
        int result = 1;
        for(int i = 1; i < length; i++){
            for(int j = 0;j < i; j++){
                if(envelopes[j][0]<envelopes[i][0] && envelopes[j][1]<envelopes[i][1]){
                    dp[i] = max(dp[i],dp[j]+1);
                }
            }
            result = max(result,dp[i]);
        }
        return result;
    }
};
```

