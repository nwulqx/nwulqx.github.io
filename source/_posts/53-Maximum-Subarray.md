---
title: 53. Maximum Subarray
date: 2018-01-27 12:33:00
tags:
- LeetCode-easy
- DP(动态规划)
- Array
---

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```java
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up:**

If you have figured out the O(*n*) solution, try coding another solution using the divide and conquer approach, which is more subtle.

<!--more-->

# 分析

这个问题比较明显，是动态规划的问题。

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/maximum-subarray/
 * Beats :  67.13%
 */
class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        dp[0] = nums[0];
        int sum = nums[0];
        for(int i = 1;i < n;i++){
            if(dp[i-1]+nums[i]>nums[i]){
                dp[i] = dp[i-1]+nums[i];
            }else{
                dp[i] = nums[i];
            }
            sum = dp[i]>sum?dp[i]:sum;
        }
        return sum;
    }
}
```

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/maximum-subarray/
 * Beats : 11.94 %;
 */
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
		vector<int> res;
		int sum = nums[0];
		res.push_back(nums[0]);
		for (int i = 1; i < nums.size(); i++){
			if (nums[i] + res[i-1] > nums[i]){
				res.push_back(nums[i] + res[i - 1]);
			}
			else{
				res.push_back(nums[i]);
			}
			sum = res[i] > sum ? res[i] : sum;
		}
		return sum;
    }
};
```

**python实现**

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        dp = []
        dp.append(nums[0])
        sum = nums[0]
        for i in range(1,len(nums)):
            if dp[i-1]+nums[i] > nums[i]:
                dp.append(dp[i - 1] + nums[i])
            else:
                dp.append(nums[i])
        sum = max(dp)
        return sum
```

# 总结

动态规划（Dynamic Programing）问题是很有意思的。总体思路其实就是循环，不过这个循环很特殊，他的当前循环的变量是根据之前的数据得出的，有很强的规划性（根据之前数据得出当前值）。总体思路是：设计一个数组存放动态规划数据，然后再在这个动态规划数组中寻找需要的数据；一般情况下可以优化，后一步查找可以在生成动态规划数组时就完成，进而省去一个循环。