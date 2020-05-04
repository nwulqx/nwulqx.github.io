---
title: 414. Third Maximum Number
date: 2018-01-30 15:16:19
tags:
- LeetCode-easy
- Array
- set(集合)
---

Given a **non-empty** array of integers, return the **third** maximum number in this array. If it does not exist, return the maximum number. The time complexity must be in O(n).

**Example 1:**

```java
Input: [3, 2, 1]

Output: 1

Explanation: The third maximum is 1.
```



**Example 2:**

```java
Input: [1, 2]

Output: 2

Explanation: The third maximum does not exist, so the maximum (2) is returned instead.
```



**Example 3:**

```java
Input: [2, 2, 3, 1]

Output: 1

Explanation: Note that the third maximum here means the third maximum distinct number.
Both numbers with value 2 are both considered as second maximum.
```

# 分析

查找第三个最大的数，这个问题以前应该碰到过类似问题，查找最大的都会，但是问题变为第三个最大的就不会了。

思路：

1. 借助一个set集合，set内部会按照有序排列，c++中只要不用unordered_set就行，这样set会自动排序这个数组，我们只需要维护这个set集合大小为3，那么其实就找出了前三个最大的数了。

2. 当然这个问题也可以用来找最小的3个数，只不过此时将从set集合的尾部删除元素。

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/third-maximum-number/
 * Beats : 100%
 * Time complicity is O(n);
 * Space complicity is O(n);
 */
class Solution {
public:
    int thirdMax(vector<int>& nums) {
		set<int> top3;
		for (int num : nums){
			top3.insert(num);
			if (top3.size() > 3){
				top3.erase(top3.begin());
			}
		}
        //注意end返回最后一个元素的下一个位置，所以要用rbegin
		return top3.size() == 3 ? *top3.begin() : *top3.rbegin();
    }
};
```

需要注意的是：`set.end()`返回的是最后一个元素的下一个位置。所以使用`set.rbegin()`

同时，`top3.erase(top3.begin());`用于删除头元素，也就是删除set中最小的元素，所以就剩下最大的3个元素了；如果此题是查找最小的3个元素，那么就变成了`top3.erase(top3.rbegin());`删除集合中最大的元素

这道题目python实现上述算法，有点困难。这里给一个网上的python作为**参考**

```python
class Solution(object):
    def thirdMax(self, nums):
        nums = sorted(list(set(nums)))
        if len(nums)<3:
            return max(nums)
        else:
            return nums[-3]
```



# 总结

set，map集合可以借助其默认有序的特点，对其保存最大n位或最小n位数，是很值得考虑的。