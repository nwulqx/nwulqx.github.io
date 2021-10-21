---
title: 55. Jump Game
date: 2021-10-21 22:42:20
tags:
- Array
- DP(动态规划)
- LeetCode-medium
---

You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` *if you can reach the last index, or* `false` *otherwise*.

 

**Example 1:**

```
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

<!--more-->

**Example 2:**

```
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
```

 

**Constraints:**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 105`

# Analysis

**c++**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/jump-game/
 * Runtime: 77 ms, faster than 43.71%
 * Memory Usage: 48.3 MB, less than 48.88%
 */
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int n = nums.size();
        int distance = 0;
        for(int i = 0; i < n && i <= distance; i++){
            distance = max(distance, nums[i]+i);
        }
        return distance >= n-1;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/jump-game/
 * Runtime: 122 ms, faster than 48.07% 
 * Memory Usage: 42.7 MB, less than 80.78%
 */
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var canJump = function(nums) {
    let distance = 0;
    for(let i = 0; i < nums.length && i <= distance; i++){
        distance = Math.max(distance,nums[i]+i);
    }
    return distance >= nums.length-1;
};
```

