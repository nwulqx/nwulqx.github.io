---
title: 78. Subsets
date: 2021-09-20 16:54:38
tags:
- Array
- LeetCode-medium
- DFS(深度优先遍历)
---

Given an integer array `nums` of **unique** elements, return *all possible subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

​     <!-- more -->

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

 

**Constraints:**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the numbers of `nums` are **unique**.

# 分析

深度优先搜索DFS

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/subsets/
 */
class Solution {
private:
    vector<int> nums;
    vector<vector<int>> res;
    vector<int> path;
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        this -> nums = nums;
        dfs(0);
        return res;
    }
    void dfs(int index) {
        res.push_back(path);
        for(int i = index; i < nums.size(); i++) {
            path.push_back(nums[i]);
            dfs(i+1);
            path.pop_back();
        }
    }
};
```

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsets = function(nums) {
    const res = [], path = [];
    function dfs(index){
        res.push([...path]);
        for(let i = index; i < nums.length; i++){
            path.push(nums[i]);
            dfs(i+1);
            path.pop();
        }
    }
    dfs(0);
    return res;
};
```

