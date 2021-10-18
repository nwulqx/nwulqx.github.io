---
title: 16. 3Sum Closest
date: 2018-02-04 11:05:49
tags:
- LeetCode-medium
- 双指针+逼近法
- Array
---

Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`.

Return *the sum of the three integers*.

You may assume that each input would have exactly one solution.

 

**Example 1:**

```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

**Example 2:**

```
Input: nums = [0,0,0], target = 1
Output: 0
```



**Constraints:**

- `3 <= nums.length <= 1000`
- `-1000 <= nums[i] <= 1000`
- `-104 <= target <= 104`

<!--more-->

# 分析

## 注意

1. 二分法和双指针法，一定不要忘了**排序**；

2. 去除重复元素。

    以上两个问题经过之前的实践，应该需要注意。

**javascript**

```js
/*
 * app:leetcode lang:javascript
 * https://leetcode.com/problems/3sum-closest
 * time completicity is O(nlogn);
 * space complicity is O(1);
 * Runtime: 104 ms, faster than 47.79%
 * Memory Usage: 40.2 MB, less than 72.34%
 */
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumClosest = function(nums, target) {
    let res = 1e9;
    const n = nums.length;
    nums.sort((a,b) => a-b);
    for(let i = 0; i < n - 2; i++){
        if(i > 0 && nums[i] === nums[i-1]) continue;
        let low = i + 1, high = n - 1;
        while(low < high){
            const sum = nums[i] + nums[low] + nums[high];
            if(Math.abs(sum-target) < Math.abs(res-target)){
                res = sum;
            }
            if(sum < target){
                low++;
                while(low < target && nums[low] === nums[low-1]) low++;
            }
            else if(sum > target){
                high--;
                while(low < target && nums[high] === nums[high+1]) high--;
            }
            else{
                return res;
            }
        }
    }
    return res;
};
```



**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/3sum-closest
 * time completicity is O(nlogn);
 * space complicity is O(1);
 * Runtime: 8 ms, faster than 84.95%
 * Memory Usage: 9.9 MB, less than 62.99%
 */
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int res = 1e9;
        int n = nums.size();
        sort(nums.begin(), nums.end());
        for(int i = 0; i < n-2; i++){
            if(i > 0 && nums[i] == nums[i-1]) continue;
            int low = i + 1, high = n - 1;
            while(low < high){
                int sum = nums[i] + nums[low] + nums[high];
                if(abs(sum-target) < abs(res-target)){
                    res = sum;
                }
                if(sum > target){
                    high--;
                    while(low < high && nums[high] == nums[high+1]) high--;
                }
                else if(sum < target){
                    low++;
                    while(low < high && nums[low] == nums[low-1]) low++;
                }
                else{
                    return res;
                }
            }
        }
        return res;
    }
};
```

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