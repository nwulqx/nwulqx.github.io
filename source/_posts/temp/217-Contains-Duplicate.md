---
title: 217. Contains Duplicate
date: 2018-01-29 15:39:04
tags:
- LeetCode-easy
- Array
---

Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

**Example 1:**

```java
Input: [1,2,3,1]
Output: true
```

**Example 2:**

```java
Input: [1,2,3,4]
Output: false
```

**Example 3:**

```java
Input: [1,1,1,3,3,4,3,2,4,2]
Output: true
```

<!--more-->

# 分析

## 方法一：利用排序

思路很简单，排序，然后找重。

**java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/contains-duplicate
 * Beats : 99.76%;
 * Time complicity is O(nlogn);
 * Space complicity is O(1);
 */
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for(int i = 0;i < nums.length-1;i++){
            if(nums[i] == nums[i+1]) return true;
        }
        return false;
    }
}
```

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/contains-duplicate
 * Beats : 28.08%;
 * Time complicity is O(nlogn);
 * Space complicity is O(1);
 */
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        //这里强制类型转换了下，要不会报错，不知道为什么，可能是c++版本问题
        for(int i = 0;i < (int)(nums.size())-1;i++){
            if(nums[i]==nums[i+1]) return true;
        }
        return false;
    }
};
```

**python实现**

```python
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        nums = sorted(nums)
        for i in range(0,len(nums)-1):
            if nums[i] == nums[i+1]:
                return True;
        return False
```



## 方法二：利用Set

我个人比较推荐使用Set，因为这样的时间复杂度为$O(n)$，用空间换了时间。

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/contains-duplicate
 * Beats : 58.85%;
 * Time complicity is O(n);
 * Space complicity is O(n);
 */
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> hash = new HashSet<Integer>(); 
        for(int i = 0;i < nums.length;i++){
            if(hash.contains(nums[i])) return true;
            hash.add(nums[i]);
        }
        return false;
    }
}
```



**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/contains-duplicate
 * Beats : 11.58%;
 * Time complicity is O(n);
 * Space complicity is O(n);
 */
class Solution {
public:
	bool containsDuplicate(vector<int>& nums) {
		set<int> hash;
		for (int i = 0; i < nums.size(); i++){
			if (hash.find(nums[i]) != hash.end()){
				return true;
			}
			else{
				hash.insert(nums[i]);
			}
		}
		return false;
	}
};
```

**python实现**

如果按照上述的思路，python会超时。看了一些比较巧妙地解法。

```python
class Solution:
    def containsDuplicate(self, nums):
        return len(nums) > len(set(nums))
    
    	"""
        超时
        hash = []
        for i in range(0, len(nums)):
            if nums[i] in hash:
                return True
            else:
                hash.append(nums[i])
        return False
        """
```

