---
title: 300. Longest Increasing Subsequence
date: 2021-03-07 17:24:54
tags:
- DP(动态规划)
- LIS(最长上升子序列)
---

Given an integer array nums, return the length of the longest strictly increasing subsequence.

A subsequence is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, `[3,6,2,7]` is a subsequence of the array `[0,3,1,6,2,2,7]`.

 <!--more-->

**Example 1:**

> Input: nums = [10,9,2,5,3,7,101,18]
> Output: 4
> Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

**Example 2:**

> Input: nums = [0,1,0,3,2,3]
> Output: 4

**Example 3:**

> Input: nums = [7,7,7,7,7,7,7]
> Output: 1

**Constraints:**

- 1 <= nums.length <= 2500
- -104 <= nums[i] <= 104

**Follow up:**

- Could you come up with the O(n2) solution?
- Could you improve it to O(n log(n)) time complexity?

# Solution

dp[i]表示第i个索引结尾时的最长序列。

需要借助两个循环：

- 第一个循环目的是找出所有`i`结尾时最长序列长度
- 第二个循环目的是计算以`i`结尾时，dp[0]~dp[i-1]的最长长度（本质上是递归的迭代办法）

```c++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int length = nums.size();
        vector<int> dp(length,0);
        int result = -1;
        for(int i = 0; i < length; i++){
            dp[i] = 1;
            for(int j = 0;j < i; j++){
                if(nums[j] < nums[i]){
                    dp[i] = max(dp[i],dp[j]+1);
                }
            }
            result = max(result,dp[i]);
        }
        return result;
    }
};
```