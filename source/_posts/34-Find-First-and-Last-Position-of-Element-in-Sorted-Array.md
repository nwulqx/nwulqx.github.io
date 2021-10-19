---
title: 34. Find First and Last Position of Element in Sorted Array
date: 2021-10-19 23:44:16
tags:
- Array
- LeetCode-medium
- 二分法
---

Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

 

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

 <!-- more -->

**Example 2:**

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

**Example 3:**

```
Input: nums = [], target = 0
Output: [-1,-1]
```

 

**Constraints:**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- `nums` is a non-decreasing array.
- `-109 <= target <= 109`

# Analysis

**二分法进阶版：查找第一个大于等于x的元素**

https://war3cdota.github.io/2019/12/28/PAT%E4%B9%99%E7%BA%A790%E9%A2%98%E6%80%BB%E7%BB%93/

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/
 * Runtime: 72 ms, faster than 85.00%
 * Memory Usage: 41.3 MB, less than 5.75% 
 */
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function(nums, target) {
    const n = nums.length;
    if(n < 1) return [-1,-1];
    let low = 0, high = n - 1;
    while(low <= high){
        const mid = Math.trunc(low + (high - low)/2);
        if(nums[mid] < target){
            low = mid + 1;
        }else{
            high = mid - 1;
        }
    }
    if(low < n && nums[low] === target){
        high = low;
        while(high<n && nums[high] === nums[low]) high++;
        return [low, high-1];
    }
    return [-1,-1]
};
```

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/
 * Runtime: 7 ms, faster than 74.47%
 * Memory Usage: 13.7 MB, less than 17.88%
 */
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int n = nums.size();
        if(n < 1) return {-1,-1};
        int low = 0, high = nums.size() - 1;
        while(low <= high){
            int mid = low + (high - low)/2;
            if(nums[mid] < target){
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }
        if(low < n && nums[low] == target){
            high = low;
            while(high < nums.size() && nums[high] == nums[low]) high++;
            return {low,high-1};
        }
        return {-1,-1};
    }
};
```

