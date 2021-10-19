---
title: 33. Search in Rotated Sorted Array
date: 2021-09-20 17:55:17
tags:
- Array
- LeetCode-medium
- 二分法
---

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **rotated** at an unknown pivot index `k` (`0 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the rotation and an integer `target`, return *the index of* `target` *if it is in* `nums`*, or* `-1` *if it is not in* `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

 <!-- more -->

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

**Example 3:**

```
Input: nums = [1], target = 0
Output: -1
```

 

**Constraints:**

- `1 <= nums.length <= 5000`
- `-104 <= nums[i] <= 104`
- All values of `nums` are **unique**.
- `nums` is guaranteed to be rotated at some pivot.
- `-104 <= target <= 104`

# 分析

二分法在循环数组的使用：https://leetcode.com/problems/search-in-rotated-sorted-array/discuss/14616/C%2B%2B-binary-search-with-comments-easy-to-read-and-understand

**c++**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/search-in-rotated-sorted-array/
 */
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int low = 0, high = nums.size() - 1;
        while(low <= high){
            int mid = low + (high - low) / 2;
            if(nums[mid] == target) return mid;
            if(nums[mid] > nums[high]) {
                if(nums[mid] > target && target >= nums[low]){
                    high = mid - 1;
                }else {
                    low = mid + 1;
                }
            }else if(nums[mid] < nums[low]){
                if(nums[mid] < target && target <= nums[high]) {
                    low = mid + 1;
                }
                else {
                    high = mid - 1;
                }
            }else {
                if(nums[mid] > target){
                    high = mid - 1;
                }else {
                    low = mid + 1;
                }
            }
        }
        return -1;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/search-in-rotated-sorted-array/
 * Runtime: 84 ms, faster than 45.80%
 * Memory Usage: 40.3 MB, less than 12.32%
 */
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    let low = 0, high = nums.length-1;
    while(low <= high){
        const mid = Math.trunc(low + (high - low)/2);
        if(nums[mid] === target) return mid;
        if(nums[mid] < nums[low]){
            if(nums[mid] < target && target <= nums[high]){
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }
        else if(nums[mid] > nums[high]){
            if(nums[low] <= target && target < nums[mid]){
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }
        else{
            if(nums[mid] > target){
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }
    }
    return -1;
};
```

