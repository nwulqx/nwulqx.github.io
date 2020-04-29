---
title: 169. Majority Element
date: 2018-01-29 10:04:58
tags:
- LeetCode-easy
- Array
- Boyer-Moore Voting Algorithm（多数投票算法）
---

Share

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

```java
Input: [3,2,3]
Output: 3
```

**Example 2:**

```java
Input: [2,2,1,1,1,2,2]
Output: 2
```

# 分析

## 解法一：最少代码的办法

先排序，然后直接索引n/2索引位置，就是majority元素。

时间复杂度：$ O(nlogn) $,主要在排序上

空间复杂度：$O(1)$，由于没有借助额外空间。

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/majority-element
 * Beats : 11.58%;
 * Time complicity is O(nlogn);
 * Space complicity is O(1);
 */
class Solution {
public:
    int majorityElement(vector<int>& nums) {
		sort(nums.begin(),nums.end());
		return nums[nums.size() / 2];
    }
};
```

## 解法二：常规法HashMap

对于一个数组，需要特定条件的元素，`Map`和`Set`一直都是得力的助手。

我们可以用Map来统计所有元素的次数，然后遍历Map返回个数大于n/2的元素。

时间复杂度：$ O(n) $

空间复杂度：$O(n)$

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/majority-element
 * Beats : 10.58%;
 * Time complicity is O(n);
 * Space complicity is O(n);
 */
class Solution {
public:
    int majorityElement(vector<int>& nums) {
		int n = nums.size();
		unordered_map<int, int> hash;
		for (int i = 0; i < nums.size(); i++){
			if (hash.find(nums[i]) != hash.end()){
				hash[nums[i]]++;
			}
			else{
				hash[nums[i]] = 1;
			}
		}
		for (auto x : hash){
			if (x.second>n / 2){
				return x.first;
			}
		}
		return nums[0];
    }
};
```

## 解法三-Boyer-Moore Voting Algorithm（多数投票算法）

参考：https://leetcode.com/problems/majority-element/solution/

这个方法好在他的空间复杂度变为了$O(1)$，具体思路是设置一个count变量，用于统计当前待选主要元素个数，每次遇到相同的元素则加1，不相同则减1；当count为0时，说明需要换待选主要元素了。例如：

> [7, 7, 5, 7, 5, 1 | 5, 7 | 5, 5, 7, 7 | 7, 7, 7, 7]	7为主要元素
>
> [7, 7, 5, 7, 5, 1 | 5, 7 | 5, 5, 7, 7 | **5, 5, 5, 5**]	5为主要元素

时间复杂度：$ O(n) $

空间复杂度：$O(1)$

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/majority-element
 * Beats : 62.58%;
 * Time complicity is O(n);
 * Space complicity is O(1);
 */
class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        Integer candidate = null;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }
}
```



**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/majority-element
 * Beats : 18.59%;
 * Time complicity is O(n);
 * Space complicity is O(1);
 */
class Solution {
public:
    int majorityElement(vector<int>& nums) {
		int count = 0;
		int majority = nums[0];
		for (int i = 0; i < nums.size(); i++){
			if (count == 0){
				majority = nums[i];
			}
			count += (majority == nums[i] ? 1 : -1);
		}
		return majority;
    }
};
```

**python实现**

```python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        count = 0
        majority = nums[0]
        for i in range(0,len(nums)):
            if count == 0:
                majority = nums[i]
            if majority==nums[i]:
                count += 1
            else:
                count -= 1
        return majority

```

