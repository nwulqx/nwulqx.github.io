---
title: 31. Next Permutation
date: 2018-02-05 11:20:02
tags:
- LeetCode-medium
- 排列组合(Permutation)
- Array
---

Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be **[in-place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

`1,2,3` → `1,3,2`
`3,2,1` → `1,2,3`
`1,1,5` → `1,5,1`

<!-- more -->

# 分析

详细参见：https://leetcode.com/articles/next-permutation/

![Alt text](https://leetcode.com/media/original_images/31_Next_Permutation.gif)

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/next-permutation/
 * Time complicity is O(n);
 * Space complicity is O(1);
 * Runtime: 140 ms, faster than 10.97%
 * Memory Usage: 40.1 MB, less than 94.22%
 */
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var nextPermutation = function(nums) {
    function swap(nums,i,j){
        const temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    function reverse(nums,start,end){
        while(start < end){
            swap(nums,start,end);
            start++;
            end--;
        }
    }
    const n = nums.length;
    let i = n - 2;
    while(i >= 0 && nums[i] >= nums[i+1]) i--;
    if(i >= 0){
        let j = n - 1;
        while(j >= 0 && nums[j] <= nums[i]) j--;
        swap(nums,i,j);
    }
    reverse(nums,i+1,n-1);
};
```

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/next-permutation/
 * Beats : 58.63%
 * Time complicity is O(n);
 * Space complicity is O(1);
 */
class Solution {
public:
	void nextPermutation(vector<int>& nums) {
		int n = nums.size();
		int i = n - 2;
		while (i >= 0 && nums[i] >= nums[i + 1]){
			i--;
		}
		if (i >= 0){
			int j = n - 1;
			while (j >= 0 && nums[j] <= nums[i]){
				j--;
			}
			swap(nums[i], nums[j]);
		}
		reverse(nums.begin()+i+1,nums.end());
	}
};
```

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/next-permutation/
 * Beats : 99.99%
 * Time complicity is O(n);
 * Space complicity is O(1);
 */
class Solution {
    public void nextPermutation(int[] nums) {
        int n = nums.length - 1;
        int i = n - 1;
        while (i >= 0 && nums[i + 1] <= nums[i]) {
            i--;
        }
        if (i >= 0) {
            int j = n;
            while (j >= 0 && nums[j] <= nums[i]) {
                j--;
            }
            swap(nums, i, j);
        }
        reverse(nums, i + 1);
    }

    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    public void reverse(int[] nums, int start) {
        int end = nums.length - 1;
        while (start < end) {
            swap(nums, start, end);
            start++;
            end--;
        }
    }
}
```

**c++实现**

```c++
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/next-permutation/
 * Beats : 58.63%
 * 直接使用c++函数库
 */
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        next_permutation(nums.begin(), nums.end());
    }
};
```

**python实现**

```python
class Solution(object):
    def reverse(self, nums, start, end):
        while start < end:
            self.swap(nums,start, end)
            start += 1
            end -= 1

    def swap(self, nums, i, j):
        temp = nums[i]
        nums[i] = nums[j]
        nums[j] = temp

    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        i = len(nums) - 2
        while i >= 0 and nums[i + 1] <= nums[i]:
            i -= 1
        if i >= 0:
            j = len(nums) - 1
            while j >= 0 and nums[j] <= nums[i]:
                j -= 1
            self.swap(nums, i, j)
        self.reverse(nums, i + 1, len(nums) - 1)

```

# 总结

这个全排列问题，其实有固定的一套解决办法，没有技巧，需要配合图，来记住这个套路。