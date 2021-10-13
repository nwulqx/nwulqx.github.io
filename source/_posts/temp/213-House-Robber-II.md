---
title: 213. House Robber II
date: 2021-03-10 21:03:37
tags:
- DP(动态规划)
---

ou are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

  <!-- more -->

**Example 1:**

> Input: nums = [2,3,2]
> Output: 3
> Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.

**Example 2:**

> Input: nums = [1,2,3,1]
> Output: 4
> Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
> Total amount you can rob = 1 + 3 = 4.

**Example 3:**

> Input: nums = [0]
> Output: 0

**Constraints:**

- 1 <= nums.length <= 100
- 0 <= nums[i] <= 1000

# Solution

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size(); 
        if (n < 2) return n ? nums[0] : 0;
        // 看成两个DP来解决~
        return max(robber(nums, 0, n - 1), robber(nums, 1, n));
    }
    int robber(vector<int>& nums,int l,int r){
        int cur = 0, pre = 0;
        for(int i = l; i < r; i++){
            int temp = cur;
            cur = max(pre + nums[i], cur);
            pre = temp;
        }
        return cur;
    }
};
```

