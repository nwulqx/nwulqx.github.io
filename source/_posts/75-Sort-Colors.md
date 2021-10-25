---
title: 75. Sort Colors
date: 2021-09-20 14:27:16
tags:
- Array
- LeetCode-medium
---

Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.



**Example 1:**

```
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

   <!-- more -->

**Example 2:**

```
Input: nums = [2,0,1]
Output: [0,1,2]
```

**Example 3:**

```
Input: nums = [0]
Output: [0]
```

**Example 4:**

```
Input: nums = [1]
Output: [1]
```

 

**Constraints:**

- `n == nums.length`
- `1 <= n <= 300`
- `nums[i]` is `0`, `1`, or `2`.

 

**Follow up:** Could you come up with a one-pass algorithm using only constant extra space?

# 分析

原址操作，空间复杂度为 S(1)

参考：https://leetcode.com/problems/sort-colors/discuss/26474/Sharing-C%2B%2B-solution-with-Good-Explanation

**javascript**

```javascript
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/sort-colors/
 * Runtime: 148 ms, faster than 5.09%
 * Memory Usage: 38 MB, less than 99.64%
 */
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
    let zero = 0, second = nums.length - 1, index = 0;
    while(index <= second){
        if(nums[index] === 0){
            nums[index++] = nums[zero];
            nums[zero++] = 0;
        }
        else if(nums[index] === 2){
            nums[index] = nums[second];
             nums[second--] = 2;
        }else{
            index++;
        }
    }
};
```
**c++**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/sort-colors/
 * Runtime: 0 ms Beats : 100 %
 * Memory: 8.3 MB Beats:  68.29% 
 */
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0, high = nums.size() - 1, index = 0;
        // 注意不是low <= high
        while(index <= high){
            if(nums[index] == 1) index++;
            else if(nums[index] == 0){
                // 注意这里的逻辑，index和low均 ++
                swap(nums[low++],nums[index++]);
            }else if(nums[index] == 2){
                // 因为从high换下来的值不确定是多少，所以此时index不变
                swap(nums[high--],nums[index]);
            }
        }
    }
};
```

