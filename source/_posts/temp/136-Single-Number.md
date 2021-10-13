---
title: 136. Single Number
date: 2017-06-19 11:02:17
tags:
---
Given an array of integers, every element appears twice except for one. Find that single one.

**Note:**
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

Subscribe to see which companies asked this question

<!-- more -->

# Solution

## Solution1

>这道题目其实可以通过排序后，遍历数组，然后得到结果。

```java
public class Solution {
    public int singleNumber(int[] nums) {
        Arrays.sort(nums);
        for(int i=0;i<nums.length;i++){
            if(i%2==1&&nums[i-1]!=nums[i])
                return nums[i-1];
            continue;
        }
        if(nums.length%2==1)
            return nums[nums.length-1];
        else
            return 0;
    }
}
```
> `i%2==1` 取模操作，很好的解决了排序后每两个间不同的比较。

## Solution2

>异或操作 `^` 是很好的去除相同元素的办法。

```java
public class Solution {
    public int singleNumber(int[] nums) {
        if(nums.length==0){
            return 0;
        }
        int res = nums[0];
        for(int i=1;i<nums.length;i++){
            res ^= nums[i];
        }
        return res;
    }
}
```

# 总结

>异或操作是一个很好的去重的方法，这一点在使用的时候很方便，应该在含有偶数个去重的问题中，能够及时联想到这个操作。