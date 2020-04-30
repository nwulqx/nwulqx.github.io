---
title: 268. Missing Number
date: 2018-01-30 14:33:21
tags:
- LeetCode-easy
- Bit Manipulation(位操作)
- Array
---

Given an array containing *n* distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.

**Example 1:**

```java
Input: [3,0,1]
Output: 2
```

**Example 2:**

```java
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```

**Note**:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

<!-- more -->

# 分析

这里可以用，排序，HashSet这两种解决，但是排序的时间复杂度为$O(nlogn)$，HashSet的空间复杂度为$O(n)$，某种程度上都不是最优。所以这两种方法可以思考下。

多种方法可以参考：https://leetcode.com/problems/missing-number/solution/

## 解法一-高斯公式

众所周知，有一个小故事就是说高斯在小时候就知道计算连续序列的技巧，那就是$s_n = n(a_1+a_n)/2$

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/missing-number
 * Beats : 22.73% 
 * Time complicity is O(n);
 * Space complicity is O(1);
 */
class Solution {
public:
    int missingNumber(vector<int>& nums) {
		int n = nums.size();
		int sum = (n+1) * n / 2;
		int add = 0;
		for (int i = 0; i < n; i++){
			add += nums[i];
		}
		return sum - add;
    }
};
```

**python实现**

```python
class Solution(object):
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        sum = (n+1)*n/2
        add = 0
        for i in range(0,n):
            add += nums[i]
        return sum - add;
```

## 解法二-Bit Manipulation(位操作)

| Index | 0    | 1    | 2    | 3    |
| ----- | ---- | ---- | ---- | ---- |
| Value | 0    | 1    | 3    | 4    |

> missing = 4^ (0^0) ^ (1^1) ^ (2^3) ^ (3^4) = (4^4) ^ (3^3) ^ (1^1) ^ 2 = 0 ^ 0 ^ 0 ^2 = 2

看懂上面这个，就知道了本题可以使用位操作，借助异或操作来找出。

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/missing-number
 * Beats : 17.30%
 * Time complicity is O(n);
 * Space complicity is O(1);
 */
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        //注意这里初始值为n
		int n = nums.size();
		int miss = nums.size();
		for (int i = 0; i < n; i++){
			miss = miss^i^nums[i];
		}
		return miss;
    }
};
```

```python
class Solution(object):
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        miss = len(nums)
        for i in range(0,len(nums)):
            miss = miss ^ i ^ nums[i]
        return miss
```

# 总结

位操作是一个很好的办法，以后在很多问题上也会见到位操作的技巧，其中异或操作作为很有特点的操作，在处理一些问题上很有效。