---
title: 16. 3Sum Closest
date: 2018-02-04 11:05:49
tags:
- LeetCode-medium
- 双指针+逼近法
- Array
---

Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

**Example:**

```java
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

<!--more-->

# 分析

## 注意

1. 二分法和双指针法，一定不要忘了排序；

2. 去除重复元素。

    以上两个问题经过之前的实践，应该需要注意。

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/3sum-closest/
 * Beats :  79.71%
 * Time complicity is O(nlogn);
 * Space complicity is O(1);
 */
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length;
        int closet = nums[0] + nums[1] + nums[2];
        for (int i = 0; i < n - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1])
                continue;
            int low = i + 1, high = n - 1;
            while (low < high) {
                int sum = nums[i] + nums[low] + nums[high];
                closet = Math.abs(sum - target) < Math.abs(closet - target) ? sum : closet;
                if(sum < target) {
                    low++;
                }else if(sum > target) {
                    high--;
                }else {
                    return closet;
                }
            }
        }
        return closet;
    }
}
```



**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/3sum-closest
 * time completicity is O(nlogn);
 * space complicity is O(1);
 * beats: 39.11%;
 */
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
		sort(nums.begin(), nums.end());
		int n = nums.size();
		int closet = nums[0] + nums[1] + nums[2];
		for (int i = 0; i < n-1; i++){
			int low = i + 1, high = n - 1;
			while (low < high){
				int sum = nums[low] + nums[high] + nums[i];
                closet = abs(sum - target)<abs(closet - target) ? sum : closet;
				if (sum < target){
					low++;
				}
				else if (sum > target){
					
					high--;
				}
				else{
					return sum;
				}
			}
		}
		return closet;
    }
};
```

**python实现**

```python
class Solution(object):
    def threeSumClosest(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        nums = sorted(nums)
        n = len(nums)
        closet = nums[0] + nums[1] + nums[2]
        for i in range(0,n-2):
            if i > 0 and nums[i]==nums[i-1]:
                continue
            low = i + 1
            high = n - 1
            while low < high:
                sum = nums[i] + nums[low] + nums[high]
                if abs(sum-target) < abs(closet-target):
                    closet = sum
                if sum < target:
                    low += 1
                elif sum > target:
                    high -= 1
                else:
                    return closet
        return closet
```

# 总结

这和3sum，4sum等是一类型的题目，需要注意两点：

1. 一定要先排序
2. 对于重复元素的去重判断