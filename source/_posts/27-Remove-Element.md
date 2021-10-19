---
title: 27. Remove Element
date: 2017-03-16 16:31:05
tags:
- LeetCode-easy
- Array
---
Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:
Given input array nums = <font color='rgb(199,37,78)'>`[3,2,2,3]`</font>, val = <font color='rgb(199,37,78)'>`3`</font>

Your function should return length = 2, with the first two elements of nums being 2.
<!--more-->

# solution
>利用了和26. Remove Duplicates from Sorted Array相同的思想，时间复杂度O(n)<br>
>利用length既可以该值既可以表示索引，也可以表示索引长度，将比较重复的逻辑换成比较数组元素和val即可！

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/remove-element/
 * Runtime: 4 ms, faster than 47.03%
 * Memory Usage: 8.9 MB, less than 35.63%
 */
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int j = 0;
        for(int i = 0; i < nums.size(); i++){
            if(nums[i] != val){
                nums[j++] = nums[i];
            }
        }
        return j;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/remove-element/
 * Runtime: 106 ms, faster than 22.34%
 * Memory Usage: 38.8 MB, less than 50.01%
 */
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function(nums, val) {
    let j = 0;
    for(let i = 0; i < nums.length; i++){
        if(nums[i] !== val){
            nums[j++] = nums[i];
        }
    }
    return j;
};
```

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/remove-element/
 * Beats : 80%
 */
	public int removeElement(int[] nums, int val) {
        // length is the return array's length
        int length = 0;
        for(int i=0;i<nums.length;i++){
        	if(nums[i] == val) 
        		continue;
            //we can also use length as index to cover val
        	nums[length] = nums[i];
        	length++;
        }
        return length;
    }
```

**python实现**

```python
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        index = 0
        for i in range(len(nums)):
            if(nums[i] != val):
                nums[index] = nums[i]
                index += 1
        return index
```



# 总结

这类题目其实考察数组的操作，其目的不在于返回一个答案数组，而只是需要前n项符合答案的数组就可以了。