---
title: 189. Rotate Array
date: 2018-01-29 10:59:40
tags:
- LeetCode-easy
- Array
- reverse(反转数组)
---

Given an array, rotate the array to the right by *k* steps, where *k* is non-negative.

**Example 1:**

```java
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

**Example 2:**

```java
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

**Note:**

- Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
- Could you do it in-place with O(1) extra space?

<!-- more -->

# 分析

这个题目因为之前有了解过，所以直接就想到了反转的思路。理论上要经历暴力循环，然后才知道这个反转的策略。

**注意**：k的值首先要模上数组大小，因为k的值是会大于数组大小的。而他的意义是和`k%nums.size()`意义一样的。

**Java实现**

```java
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/majority-element
 * Beats : 100%
 * Time complicity is O(n);
 * Space complicity is O(1);
 */
class Solution {
  public void rotate(int[] nums, int k) {
    k %= nums.length;
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
  }
  public void reverse(int[] nums, int start, int end) {
    while (start < end) {
      int temp = nums[start];
      nums[start] = nums[end];
      nums[end] = temp;
      start++;
      end--;
    }
  }
}
```

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/majority-element
 * Beats : c++测试有问题，不过代码是正确的
 * Time complicity is O(n);
 * Space complicity is O(1);
 */
class Solution {
public:
	void rotate(vector<int>& nums, int k) {
		k %= nums.size();
		reverse(nums.begin(), nums.end());
		reverse(nums.begin(), nums.begin() + k);
		reverse(nums.begin() + k, nums.end());
	}
};
```

**python实现**

这里python的实现值得学习，学习了python的方法调用。

```python
class Solution(object):
    """方法的定义"""
    def reverse(self,nums,start,end):
        while start < end:
            temp = nums[start]
            nums[start] = nums[end]
            nums[end] = temp
            start += 1
            end -= 1
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k %= n
        """self.调用方法"""
        self.reverse(nums, 0, n - 1)
        self.reverse(nums, 0, k - 1)
        self.reverse(nums, k, n - 1)
```



# 总结

这种Rotate Array旋转数组的最好方法是`reverse`方法（从思路和时间空间复杂度考虑），通过三次反转数组，即可达到旋转数组的目的，这么做的好处是它可以不借助额外空间，使其空间复杂度为$O(1)$