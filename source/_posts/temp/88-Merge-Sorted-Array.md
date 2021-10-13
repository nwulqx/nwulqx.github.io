---
title: 88. Merge Sorted Array
date: 2017-04-27 18:30:46
tags:
- LeetCode-easy
- Optimize(优化)
- Array
---

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

**Note:**

You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

<!-- more -->

# 分析

>第一个想法，借助归并排序的思路。做一个中规中矩的做法。是可以通过的。

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/merge-sorted-array
 * Beats : 11.97%;
 */
public class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
    	int tmp[] = new int[n+m];
    	int i=0 , j=0 , k=0;
    	for(int index = 0;index<m+n;index++){
    		if(i==m) tmp[k++] = nums2[j++];
    		else if(j==n) tmp[k++] = nums1[i++];
    		else if(nums1[i]<nums2[j]){
    			tmp[k++] = nums1[i++];
    		}else{
    			tmp[k++] = nums2[j++];
    		}
    	}
    	int index = 0;
    	for(int num : tmp){
    		nums1[index++] = num;
    	}
    }
}
```
但是，借助另一个空间，空间复杂度O(n)

## 优化

其实这道题条件就已经指出了结果，m指前m个nums1元素，n指前n个nums2元素。也就是已经给出了带合并的两个数组长度，且第一个数组空出了合并第二个数组的位置，那么其实就是让你把两个数组合并到nums1上。
那之前为什么借助了一个数组作为临时数组，其实是为了解决最坏情况。
考虑一个情景：

>nums1 = [1,2,3,4] m=2;
>nums2 = [5,6,7,8] n=2;

按照要求，是[1,2]和[5,6]的排序，那如果不借助临时数组，在nums1中直接排序，则[5,6]会覆盖[1,2]的位置。

**但是换一个思路，如果用倒序的顺序排序呢？**

那就可以省去这个临时数组了，不需要考虑覆盖的问题了。

[1,2]和[5,6]可以排下，并且由于题设nums1的大小是一定大于m+n的。所以倒序是可行的，并且节省了**空间复杂度**。

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/merge-sorted-array
 * Beats : 100 %;
 */
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        m--;
        n--;
        int i = nums1.length - 1;
        while(m>=0 || n>=0){
            if(m<0){
                nums1[i--] = nums2[n--];
            }else if(n<0){
                nums1[i--] = nums1[m--];
            }else if(nums1[m]>nums2[n]){
                nums1[i--] = nums1[m--];
            }else{
                nums1[i--] = nums2[n--];
            }
        }
    }
}
```

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/merge-sorted-array
 * Beats : 11.97%;
 */
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
		int i = nums1.size() - 1;
		m--, n--;
		while (i >= 0){
			while (m >= 0 || n >= 0){
				if (m < 0){
					nums1[i--] = nums2[n--];
				}
				else if (n < 0){
					nums1[i--] = nums1[m--];
				}
				else if (nums1[m] > nums2[n]){
					nums1[i--] = nums1[m--];
				}
				else{
					nums1[i--] = nums2[n--];
				}
			}
		}
    }
};
```

**python实现**

```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: None Do not return anything, modify nums1 in-place instead.
        """
        m -= 1
        n -= 1
        i = len(nums1) - 1
        while m>=0 or n >= 0:
            if m < 0:
                nums1[i] = nums2[n]
                n -= 1
            elif n < 0:
                nums1[i] = nums1[m]
                m -= 1
            elif nums1[m] > nums2[n]:
                nums1[i] = nums1[m]
                m -= 1
            else:
                nums1[i] = nums2[n]
                n -= 1
            i -= 1
```



# 总结

>这题其实考察了归并排序中的一个知识点：合并两个数组，在这个基础上对其进行了一个小优化，由于之前学过归并排序，思路是有的，但是这个问题其实是可以不借助临时数组的。由于他的特殊性，倒序排序不会导致它的所需排序的元素被覆盖，这是应该注意的。