---
title: 128. Longest Consecutive Sequence
date: 2021-09-20 18:40:22
tags:
- Array
- LeetCode-medium
- Optimize(优化)
---

Given an unsorted array of integers `nums`, return *the length of the longest consecutive elements sequence.*

You must write an algorithm that runs in `O(n)` time.

 <!-- more -->

**Example 1:**

```
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

**Example 2:**

```
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

 

**Constraints:**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`

# 分析

这道题目要求时间复杂度为O(n)，那么肯定不能排序，所以只好用Set来处理查找。思路比较简单，注意的是：优化，如果某个元素作为一条路径查找过了，就不需要了，**这个判断可以通过对其前面一个元素的查找来判断~**

参考：https://leetcode.com/problems/longest-consecutive-sequence/discuss/41057/Simple-O(n)-with-Explanation-Just-walk-each-streak

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/triangle/
 */
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> st(nums.begin(), nums.end());
        int res = 0;
        for(int n : nums){
            // 优化点
            if(st.find(n-1) == st.end()){
                int y = n+1;
                while(st.find(y) != st.end()){
                    y++;
                }
                res = max(res,y-n);
            }
        }
        return res;
    }
};
```

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var longestConsecutive = function(nums) {
    const st = new Set(nums);
    let res = 0;
    for(let i = 0; i < nums.length; i++){
        let n = nums[i];
        // 优化点，之前没找过的才作为start开始找
        if(!st.has(n-1)){
            while(st.has(n)){
                n++
            }
            res = Math.max(res,n - nums[i]); 
        }
    }
    return res;
};
```

