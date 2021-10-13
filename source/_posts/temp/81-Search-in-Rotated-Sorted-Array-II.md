---
title: 81. Search in Rotated Sorted Array II
date: 2021-09-20 18:06:00
tags:
- Array
- LeetCode-medium
- 二分法
---

There is an integer array `nums` sorted in non-decreasing order (not necessarily with **distinct** values).

Before being passed to your function, `nums` is **rotated** at an unknown pivot index `k` (`0 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,4,4,5,6,6,7]` might be rotated at pivot index `5` and become `[4,5,6,6,7,0,1,2,4,4]`.

Given the array `nums` **after** the rotation and an integer `target`, return `true` *if* `target` *is in* `nums`*, or* `false` *if it is not in* `nums`*.*

You must decrease the overall operation steps as much as possible.

​       <!-- more -->

**Example 1:**

```
Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true
```

**Example 2:**

```
Input: nums = [2,5,6,0,0,1,2], target = 3
Output: false
```

 

**Constraints:**

- `1 <= nums.length <= 5000`
- `-104 <= nums[i] <= 104`
- `nums` is guaranteed to be rotated at some pivot.
- `-104 <= target <= 104`

 

**Follow up:** This problem is similar to [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/), but `nums` may contain **duplicates**. Would this affect the runtime complexity? How and why?

# 分析

参考：https://leetcode.com/problems/search-in-rotated-sorted-array-ii/discuss/28218/My-8ms-C%2B%2B-solution-(o(logn)-on-average-o(n)-worst-case)

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/search-in-rotated-sorted-array-ii/
 */
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        int low = 0, high = nums.size() - 1;
        while(low <= high){
            int mid = low + (high - low)/2;
            if(nums[mid] == target) return true;
            if(nums[mid] == nums[low] && nums[mid] == nums[high]){
                low++;
                high--;
            }
            else if(nums[mid] < nums[low]){
                if(target > nums[mid] && target <= nums[high]){
                    low = mid + 1;
                }
                else{
                    high = mid - 1;
                }
            }
            else if(nums[mid] > nums[high]){
                if(target >= nums[low] && target < nums[mid]){
                    high = mid - 1;
                }
                else{
                    low = mid + 1;
                }
            }else {
                if(target < nums[mid]){
                    high = mid - 1;
                }else{
                    low = mid + 1;
                }
            }
        }
        return false;
    }
};
```



```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {boolean}
 */
var search = function(nums, target) {
    let low = 0, high = nums.length - 1;
    while(low <= high){
        let mid = Math.floor(low + (high - low)/2);
        if(nums[mid] === target) return true;
        if(nums[mid] === nums[low] && nums[mid] === nums[high]){
            low++;
            high--;
        }
        else if(nums[mid] > nums[high]){
            if(target >= nums[low] && target < nums[mid]){
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }
        else if(nums[mid] < nums[low]){
            if(target > nums[mid] && target <= nums[high]){
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }else {
            if(target < nums[mid]){
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }
    }
    return false;
};
```

