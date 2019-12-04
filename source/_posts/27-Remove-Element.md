---
title: 27. Remove Element
date: 2017-03-16 16:31:05
tags:
- LeetCode-easy
- Optimize(优化)
---
Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:
Given input array nums = <font color='rgb(199,37,78)'>`[3,2,2,3]`</font>, val = <font color='rgb(199,37,78)'>`3`</font>

Your function should return length = 2, with the first two elements of nums being 2.
<!--more-->

# solution
>利用了和RemoveDuplicatesfromSortedArray相同的思想，时间复杂度O(n)<br>
>利用length既可以该值既可以表示索引，也可以表示索引长度，将比较重复的逻辑换成比较数组元素和val即可！

```java
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

# 思考

>这道题目我隐约记得，以前在解决JavaScript中的数组删除指定或者相同元素时，使用过这种类似的方法，虽然数组大小不改变，但是使用了一个值来记录所需要的数组长度，并把该长度内不需要的元素删除并替换。<br>

**补充：**

>看到了解析后，我觉得我想的不够全面，这道题解法到此为止了么，还可以优化么？最好情况或者最差情况是什么？平均的复杂度怎么样？

考虑一个最坏情况：

	nums = [1,2,3,5,4], val = 4

```java
public class Solution {
    public int removeElement(int[] nums, int val) {
        int i = -1;
        int n = nums.length-1;
        while(i<n){
            if(nums[i+1]==val){
                nums[i+1] = nums[n--];
            }else{
                i++;
            }
        }
        return i+1;
    }
}
```

P.S.对索引的操作应该极为小心。