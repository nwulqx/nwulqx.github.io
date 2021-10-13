---
title: 167. Two Sum II - Input array is sorted
date: 2018-01-28 18:36:36
tags:
- LeetCode-easy
- Array
- 双指针+逼近法
---

Given an array of integers that is already ***sorted in ascending order\***, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

**Note:**

- Your returned answers (both index1 and index2) are not zero-based.
- You may assume that each input would have *exactly* one solution and you may not use the *same* element twice.

**Example:**

```java
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```

<!-- more -->

# 分析

这道题目，一上来告诉你是有序数组，那其实想到了两个和有序有关的算法：二分法和双指针，但二分法是查找单个元素。那可以确定是`双指针`方法来计算了。当然这道题目，仍可以参考`1.TwoSum`的HashMap的方法，不过有了双指针这个利器，感觉双指针从易用性和理解性更优秀。

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/
 * Beats : 40%;
 */
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int low = 0;
        int high = numbers.length-1;
        while(low<high){
        	if(numbers[low]+numbers[high]>target){
        		high--;
        	}else{
        		if(numbers[low]+numbers[high]<target){
        			low++;
        		}else{
        			return new int[]{low+1,high+1};
        		}
        	}
        }
        return new int[]{};
    }
}
```

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/
 * Beats : 94.25 %;
 */
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
		int low = 0, high = numbers.size() - 1;
		vector<int> result;
		while (low < high){
			if (numbers[low] + numbers[high]>target){
				high--;
			}
			else if (numbers[low] + numbers[high] < target){
				low++;
			}
			else{
				result.push_back(low+1);
				result.push_back(high+1);
				return result;
			}
		}
		return result;
    }
};
```

**python实现**

```python
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        low = 0
        high = len(numbers)-1
        while low < high:
            if numbers[low] + numbers[high] < target:
                low += 1
            elif numbers[low] + numbers[high] > target:
                high -= 1
            else:
                return [low+1,high+1]
        return []
```

# 总结

双指针的使用条件，要注意是有序数组，不是有序数组不能使用双指针和二分法，这点一定要注意。