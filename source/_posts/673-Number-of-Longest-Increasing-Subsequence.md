---
title: 673. Number of Longest Increasing Subsequence
date: 2021-03-07 17:30:38
tags:
- DP(动态规划)
- LIS(最长上升子序列)
---

Given an integer array nums, return the number of longest increasing subsequences.

Notice that the sequence has to be strictly increasing.

 <!--more-->

**Example 1:**

> Input: nums = [1,3,5,4,7]
> Output: 2
> Explanation: The two longest increasing subsequences are [1, 3, 4, 7] and [1, 3, 5, 7].

**Example 2:**

> Input: nums = [2,2,2,2,2]
> Output: 5
> Explanation: The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.

 

**Constraints:**

- 1 <= nums.length <= 2000
- -106 <= nums[i] <= 106



# Solution

求解最长子序列的个数，注意需要另一个状态来保存每一个以i为结尾的序列的个数。

```c++
class Solution {
public:
    int findNumberOfLIS(vector<int>& nums) {
        int length = nums.size();
        vector<int> dp(length,1);
        vector<int> cnt(length,1);
        int maxLen = 1;
        int result = 0;
        for(int i = 1;i < length; i++){
            for(int j = 0;j < i; j++){
                if(nums[j] < nums[i]){
                    if(dp[i] < dp[j]+1){
                        dp[i] = dp[j]+1;
                        cnt[i] = cnt[j]; // 注意这里的状态转移
                    }else if(dp[i] == dp[j]+1){
                        cnt[i] += cnt[j];
                    }
                }
            }
            maxLen = dp[i]>maxLen?dp[i]:maxLen;
        }
        for(int i = 0;i < length;i++){
            result += (dp[i]==maxLen?cnt[i]:0);
        }
        return result;
    }
};
```