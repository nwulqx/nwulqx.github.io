---
title: 152. Maximum Product Subarray
date: 2021-03-07 17:23:05
tags:
- DP(动态规划)
- 最大子数组和
- Array
- LeetCode-medium
---

Given an integer array nums, find a contiguous non-empty subarray within the array that has the largest product, and return the product.

It is guaranteed that the answer will fit in a 32-bit integer.

A subarray is a contiguous subsequence of the array.

 <!-- more -->

**Example 1:**

> Input: nums = [2,3,-2,4]
> Output: 6
> Explanation: [2,3] has the largest product 6.

**Example 2:**

> Input: nums = [-2,0,-1]
> Output: 0
> Explanation: The result cannot be 2, because [-2,-1] is not a subarray.

**Constraints:**

- 1 <= nums.length <= 2 * 104
- -10 <= nums[i] <= 10

# Solution

注意这道题目对于负数是要处理的，因为两个负数相乘是负数，所以要考虑：

- 使用一个minDP的DP数组，用来存储负数最小的值，因为负数最小的值，乘以一个负数会变成最大的正数

```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int length = nums.size();
        vector<int> minDP(nums),maxDP(nums);
        int result = nums[0];
        for(int i = 1;i < length;i++){
            // 这里的逻辑要认真考虑
            maxDP[i] = max(minDP[i-1]*nums[i],max(nums[i],maxDP[i-1]*nums[i]));
            minDP[i] = min(minDP[i-1]*nums[i],min(nums[i],maxDP[i-1]*nums[i]));
            result = max(result,maxDP[i]);
        }
        return result;
    }
};
```

二刷

参考：https://leetcode.com/problems/maximum-product-subarray/discuss/48230/Possibly-simplest-solution-with-O(n)-time-complexity

```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int res = nums[0];
        for(int i = 1,rmin = res,rmax = res; i < nums.size(); i++){
            if(nums[i] < 0){
                swap(rmin, rmax);
            }
            rmax = max(nums[i],rmax*nums[i]);
            rmin = min(nums[i],rmin*nums[i]);
            res = max(rmax,res);
        }
        return res;
    }
};
```

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxProduct = function(nums) {
    let res = nums[0], rmin = nums[0], rmax = nums[0];
    for(let i = 1; i < nums.length; i++){
        if(nums[i] < 0){
            const temp = rmin;
            rmin = rmax;
            rmax = temp;
        }
        rmax = Math.max(nums[i],nums[i]*rmax);
        rmin = Math.min(nums[i],nums[i]*rmin);
        
        res = Math.max(res,rmax);
    }
    return res;
};
```

