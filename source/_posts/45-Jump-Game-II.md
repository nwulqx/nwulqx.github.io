---
title: 45. Jump Game II
date: 2021-10-20 22:46:48
tags:
---

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

 

**Example 1:**

```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

 <!-- more -->

**Example 2:**

```
Input: nums = [2,3,0,1,4]
Output: 2
```

 

**Constraints:**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 1000`

# Analysis

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/jump-game-ii/
 * Runtime: 112 ms, faster than 57.49%
 * Memory Usage: 40.5 MB, less than 86.72%
 */
/**
 * @param {number[]} nums
 * @return {number}
 */
var jump = function(nums) {
    let start = 0, end = 0, step = 0, maxEnd = 0, n = nums.length;
    while(end < n - 1){
        step++;
        for(let i = start; i <= end; i++){
            maxEnd = Math.max(maxEnd,nums[i]+i);
        }
        start = end + 1;
        end = maxEnd;
    }
    return step;
};
```

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/jump-game-ii/
 * Runtime: 32 ms, faster than 48.11%
 * Memory Usage: 16.3 MB, less than 71.58%
 */
class Solution {
public:
    int jump(vector<int>& nums) {
        int n = nums.size(), step = 0, start = 0, end = 0, maxEnd = 0;
        while(end < n-1){
            step++;
            for(int i = start; i <= end; i++){
                maxEnd = max(maxEnd,nums[i]+i);
            }
            start = end + 1;
            end = maxEnd;
        }
        return step;
    }
};
```

