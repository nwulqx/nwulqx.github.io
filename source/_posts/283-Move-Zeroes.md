---
title: 283. Move Zeroes
date: 2018-01-30 15:07:44
tags:
- LeetCode-easy
- Array
---

Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```java
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note**:

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations.

# 分析

这个问题想复杂了，其实很简单，设置一个索引把非零数按序重新按序排列，最后将后面补0

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/move-zeroes
 * Beats : 99.83%
 * Time complicity is O(n);
 * Space complicity is O(1);
 */
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
		int index = 0;
		int n = nums.size();
		for (int i = 0; i < n; i++){
			if (nums[i] != 0){
				nums[index++] = nums[i];
 			}
		}
		for (int j = index; j < n; j++){
			nums[j] = 0;
		}
    }
};
```

**python实现**

```python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        index = 0
        for i in range(0,len(nums)):
            if nums[i] != 0:
                nums[index] = nums[i]
                index += 1
        for i in range(index,len(nums)):
            nums[i] = 0
```

# 总结

有时候，这种问题很简单，不要把它想得太难了，直接遍历可能会很容易。