---
title: 162. Find Peak Element
date: 2021-09-20 19:56:02
tags:
- Array
- LeetCode-medium
- 二分法
---

A peak element is an element that is strictly greater than its neighbors.

Given an integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`.

You must write an algorithm that runs in `O(log n)` time.

  <!-- more -->

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

**Example 2:**

```
Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.
```

 

**Constraints:**

- `1 <= nums.length <= 1000`
- `-231 <= nums[i] <= 231 - 1`
- `nums[i] != nums[i + 1]` for all valid `i`.

# 分析

这题目比较差，能跑就行了，需要先判断开头和结尾，如果直接可以获得一种结果，则直接返回就行了~否则再用二分去找

参考：https://leetcode.com/problems/find-peak-element/discuss/1290642/intuition-behind-conditions-complete-explanation-diagram-binary-search （写的比较清楚）

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/find-peak-element/
 */
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        if(nums.size() == 1) return 0; // single element
        
        int n = nums.size();
		// check if 0th/n-1th index is the peak element
        if(nums[0] > nums[1]) return 0;
        if(nums[n-1] > nums[n-2]) return n-1;
        int low = 1, high = nums.size() - 2;
        while(low <= high){
            int mid = low + (high - low)/2;
            if(nums[mid] > nums[mid-1] && nums[mid] > nums[mid+1]){
                return mid;
            }
            if(nums[mid] < nums[mid-1]) {
                high = mid - 1;
            }else if(nums[mid] < nums[mid+1]){
                low = mid + 1;
            } 
        }
        return -1;
    }
};
```



```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findPeakElement = function(nums) {
    let n = nums.length, low = 1, high = nums.length - 2;
    if(nums.length === 1) return 0;
    if(nums[0] > nums[1]) return 0;
    if(nums[n-1] > nums[n-2]) return n-1;
    while(low <= high){
        let mid = Math.trunc(low + (high - low)/2);
        if(nums[mid] > nums[mid-1] && nums[mid] > nums[mid+1]) return mid;
        else if(nums[mid] < nums[mid-1]) high = mid - 1;
        else if(nums[mid] < nums[mid+1]) low = mid + 1;
    }
    return -1;
};
```

