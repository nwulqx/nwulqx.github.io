---
title: 26. Remove Duplicates from Sorted Array
date: 2017-03-16 16:19:33
tags:
- LeetCode-easy
- Array
---
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,
Given input array nums = <font color='rgb(199,37,78)'>`[1,1,2]`</font>,

Your function should return length = <font color='rgb(199,37,78)'>`2`</font>, with the first two elements of nums being <font color='rgb(199,37,78)'>`1`</font> and <font color='rgb(199,37,78)'>`2`</font> respectively. It doesn't matter what you leave beyond the new length.

<!--more-->

# solution

>去除重复元素，并返回数组长度。<br/>
>注意：这题并不是真正的让你删除重复元素，题目要求你只是返回结果的数组长度length，并在输入数组的基础上改写前length项为不相同数据。<br/>
>需要设置一个长度length（该值既可以表示索引，也可以表示索引长度），遍历数组，当数组相邻元素重复时，将当前索引处的值赋给length为索引处，同时length++；<br>
>遍历完成后，返回length。

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/remove-duplicates-from-sorted-array/submissions/
 * Beats : 99%
 */
class Solution {
    public int removeDuplicates(int[] nums) {
        int index = 1;
        for(int i = 1;i < nums.length;i++){
            if(nums[i] == nums[i-1]){
                continue;
            }
            nums[index++] = nums[i];
        }
        return index;
    }
}
```

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/remove-duplicates-from-sorted-array/submissions/
 * Beats : 98.54%
 */
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
		if (nums.size() < 2) return nums.size();
		int index = 1;
		for (int i = 1; i < nums.size(); i++){
			if (nums[i] == nums[i - 1]){
				continue;
			}
			nums[index++] = nums[i];
		}
		return index;
    }
};
```

**python实现**

```python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        index = 1
        for i in range(1,len(nums)):
            if nums[i] == nums[i-1]:
                continue
            else:
                nums[index] = nums[i]
                index += 1
        return index
```

