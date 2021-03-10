---
title: 198. House Robber
date: 2021-03-10 21:02:23
tags:
- DP(动态规划)
---

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

 <!-- more -->

**Example 1:**

> Input: nums = [1,2,3,1]
> Output: 4
> Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
> Total amount you can rob = 1 + 3 = 4.

**Example 2:**

> Input: nums = [2,7,9,3,1]
> Output: 12
> Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
> Total amount you can rob = 2 + 9 + 1 = 12.

**Constraints:**

- 1 <= nums.length <= 100
- 0 <= nums[i] <= 400

# Solution

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        int length = nums.size();
        if(length < 2) return length ? nums[0] : 0;
        int cur = 0, pre = 0;
        for(int i = 0; i < length; i++){
            // 这块的逻辑很巧妙，巧妙地解决了前两个数的问题
            int tmp = cur;
            cur = max(pre+nums[i],cur);
            pre = tmp;
        }
        return cur;
    }
};
```

