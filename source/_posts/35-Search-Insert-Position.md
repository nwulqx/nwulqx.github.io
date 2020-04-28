---
title: 35. Search Insert Position
date: 2018-01-07 10:59:38
tags:
- LeetCode-easy
- Array
- 二分法
---

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

**Example 1:**

```java
Input: [1,3,5,6], 5
Output: 2
```

**Example 2:**

```java
Input: [1,3,5,6], 2
Output: 1
```

**Example 3:**

```java
Input: [1,3,5,6], 7
Output: 4
```

**Example 4:**

```java
Input: [1,3,5,6], 0
Output: 0
```

<!--more-->



# 分析

这道题目是针对有序数组，那么适用二分法解决。

# 二分查找

二分查找的基本思路不用再说了，注意几个点：

- 虽然查找条件`while(low<=high)`也可以写成`while(low<high)`，但是有区别，前者未找到时，low和high处于第一次`low>high`的状态；而后者处于`low==high`的状态。这里统一下，用第一种方法，后面会说为什么这么做。

- 总是在low~mid-1和mid+1~high之间查找元素。对于mid判断完毕后，不用再包含mid。

**二分查找基准（查找不到返回-1）**

```c++
//A为递增数列，x为欲查询的数，函数返回查找到的索引，未查找到返回-1
int binarySearch(int a[],int low,int high,int x){
	while (low <= high){
		int mid = low + (high - low) / 2;
		if (a[mid] < x){
			low = mid + 1;
		}
		else if (a[mid] > x){
			high = mid - 1;
		}
		else
			return mid;
	}
	return -1;
}

```

# 二分查找扩展

基于二分查找，可以进一步扩展两个方法。

- 查找第一个大于或等于x的元素位置

- 查找第一个大于x的元素位置

## 查找第一个大于或等于x的元素位置

原理比较简单，只需要对分支判断中的等于做相应处理即可。

**查找第一个大于或等于x的元素位置基准代码**

```c++
//A为递增数列，x为欲查询的数，函数返回查找到的索引，未查找到返回-1
int binarySearch(int a[],int low,int high,int x){
	while (low <= high){
		int mid = low + (high - low) / 2;
		if (a[mid] < x){
			low = mid + 1;
		}
		else if (a[mid] >= x){
			high = mid - 1;
		}
	}
	return low;
}
```

这里修改了三处：第一，修改了`return -1`为`return low`；第二，修改条件`if (a[mid] > x)`为`if (a[mid] >= x)`；第三，删除条件`return mid`。

**分析：**

查找第一个大于或等于x的元素位置，将条件`if (a[mid] > x)`改为`if (a[mid] >= x)`，对于只要大于等于x的位置，都在其左半部分查找（**降低high**）。该条件会导致高位high不断向左靠近，直到最后一个小于x的位置。

**最终，high和low均指向最后一个小于x的位置。这里要解释下上面为什么while条件中使用`(low<=high)`，当`while (low == high)`成立，条件满足`if (a[mid] < mp) low = mid + 1;`，所以最终能通过low返回第一个大于等于x的索引位置。其目的就是为了保证low在等于high（指向最后一个小于x的位置）时，仍可以多一步运算而指向第一个大于等于的元素。**

## 查找第一个大于x的元素位置

同上。只不过等于号加在另一个条件中。

**查找第一个大于x的元素位置基准代码**

```c++
//A为递增数列，x为欲查询的数，函数返回查找到的索引，未查找到返回-1
int binarySearch(int a[],int low,int high,int x){
	while (low <= high){
		int mid = low + (high - low) / 2;
		if (a[mid] <= x){
			low = mid + 1;
		}
		else if (a[mid] > x){
			high = mid - 1;
		}
	}
	return low;
}

```

与上面唯一的不同在于将等号放在了条件`if (a[mid] <= x)`中，但是却将最终结果变成了查找第一个大于x的元素位置。

**分析：**

此时，对于小于等于x的情况，都是在右半部分查找（提高low），该条件会导致低位low不断向右靠近，直到最后一个小于或等于x的位置。
当（low==high）时，将`low = mid+1`，最终将返回第一个大于x的位置索引。

## 二分查找，将未找到的元素插入到合适位置

这个问题其实是**查找第一个大于或等于x的元素位置**的不同问法而已。本质是一样的。

那么这道题目就是**查找第一个大于或等于x的元素位置**。

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/search-insert-position
 * Beats : 90%;
 */
class Solution {
    public int searchInsert(int[] nums, int target) {
        int low = 0,high = nums.length-1,mid;
        while(low <= high){
            mid = low + (high-low)/2;
            if(nums[mid] < target){
                low = mid+1;
            }else if(nums[mid] >= target){
                high = mid-1;
            }
        }
        return low;
    }
}
```



**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/search-insert-position
 * Beats : 90%;
 */
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
		int low = 0, high = nums.size() - 1, mid;
		while (low <= high){
			mid = low + (high - low) / 2;
			if (target > nums[mid]){
				low = mid + 1;
			}
			else{
				high = mid - 1;
			}
		}
		return low;
    }
};
```

python实现

```python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        low = 0
        high = len(nums)-1
        while(low<=high):
            mid = low + (high-low)/2
            if(target <= nums[mid]):
                high = mid - 1;
            else:
                low = mid + 1;
        return low
```



# 总结

对于二分查找题目，只要判断可以用二分查找解决，那么其实可以先实现二分查找，再根据需要看看是实现：

- 查找第一个大于或等于x的元素位置（等价于**将未找到的元素插入到合适位置**）

- 查找第一个大于x的元素位置

这两个情况的哪一个，具体只需要看看等号是加在哪个条件上就可以决定不同的结果了。