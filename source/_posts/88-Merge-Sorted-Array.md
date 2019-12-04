---
title: 88. Merge Sorted Array
date: 2017-04-27 18:30:46
tags:
- LeetCode-easy
- Optimize(优化)
---

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

**Note:**

You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

<!-- more -->
# Solution

## Solution1

>第一个想法，借助归并排序的思路。是一个中规中矩的做法。是可以通过的。

```java
public class MergeSortedArray2{
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int mergeArray[] = new int[m+n];
        int index1 = 0;
        int index2 = 0;
        for(int i=0;i<mergeArray.length;i++){
            if(index1>=m){
                mergeArray[i] = nums2[index2++];
            }else if(index2>=n){
                mergeArray[i] = nums1[index1++];
            }else{
                if(nums1[index1]<nums2[index2]){
                    mergeArray[i] = nums1[index1++];
                }else{
                    mergeArray[i] = nums2[index2++];
                }
            }
        }
        for(int j=0;j<mergeArray.length;j++){
            nums1[j] = mergeArray[j];
        }
        return mergeArray;
    }
}
```
但是，借助另一个空间，空间复杂度O(n)

## Optimized

其实这道题需求有点奇怪，m指前m个nums1元素，n指前n个nums2元素。
那之前为什么借助了一个数组作为临时数组，其实是为了解决最坏情况。
考虑一个情景：

>nums1 = [1,2,3,4] m=2;
>nums2 = [5,6,7,8] n=2;

按照要求，是[1,2]和[5,6]的排序，那如果不借助临时数组，在nums1中直接排序，则[5,6]会覆盖[1,2]的位置。

**但是换一个思路，如果用倒序的顺序排序呢？**

那就可以省去一个临时数组。

[1,2]和[5,6]可以排下，并且由于题设nums1的大小是一定大于m+n的。所以倒序是可行的，并且节省了空间复杂度。

```java
public class MergeSortedArray{
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m-1;
        int j = n-1;
        for(int k=m+n-1;k>=0;k--){
            if(i<0&&j>=0){
                nums1[k] = nums2[j--];
            }else if(j<0){
                break;
            }else{
                if(nums1[i]>nums2[j]){
                    nums1[k] = nums1[i--];
                }else{
                    nums1[k] = nums2[j--];
                }
            }
        }
    }
}
```

# 总结
>这题其实考的还是优化，由于之前学过归并排序，思路是有的，但是这个问题其实是可以不借助临时数组的。由于他的特殊性，倒序排序不会导致它的所需排序的元素被覆盖，这是应该注意的。