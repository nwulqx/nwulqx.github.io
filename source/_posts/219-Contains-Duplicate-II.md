---
title: 219. Contains Duplicate II
date: 2018-01-29 16:18:17
tags:
- LeetCode-easy
- Array
---

Given an array of integers and an integer *k*, find out whether there are two distinct indices *i* and *j* in the array such that **nums[i] = nums[j]** and the **absolute** difference between *i* and *j* is at most *k*.

**Example 1:**

```java
Input: nums = [1,2,3,1], k = 3
Output: true
```

**Example 2:**

```java
Input: nums = [1,0,1,1], k = 1
Output: true
```

**Example 3:**

```java
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```

# 分析

使用HashMap做就可以了。

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/contains-duplicate-ii
 * Beats : 89.19%
 * Time complicity is O(n);
 * Space complicity is O(n);
 */
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Map<Integer,Integer> hash = new HashMap<Integer,Integer>();
        for(int i = 0;i < nums.length;i++){
            if(hash.containsKey(nums[i])){
                if(i - hash.get(nums[i]) <= k){
                    return true;
                }
                else{
                    hash.put(nums[i],i);
                }
            }
            else{
                hash.put(nums[i],i);
            }
        }
        return false;
    }
}
```

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/contains-duplicate-ii
 * Beats : 26.57% 
 * Time complicity is O(n);
 * Space complicity is O(n);
 */
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
		unordered_map<int, int> hash;
		for (int i = 0; i < nums.size(); i++){
			if (hash.find(nums[i]) != hash.end()){
				if (i - hash[nums[i]] <= k){
					return true;
				}
				else{
					hash[nums[i]] = i;
				}
			}
			else{
				hash[nums[i]] = i;
			}
		}
		return false;
    }
};
```

**python实现**

```python
class Solution(object):
    def containsNearbyDuplicate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        hash = {}
        for i in range(0,len(nums)):
            if nums[i] in hash:
                if i - hash[nums[i]] <= k:
                    return True
                else:
                    hash[nums[i]] = i
            else:
                hash[nums[i]] = i
        return False
```

# 总结

Map和Set是解决数组类问题的得力工具，必要的时候很值得考虑。