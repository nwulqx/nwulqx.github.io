---
title: 90. Subsets II
date: 2021-09-20 18:15:50
tags:
- Array
- LeetCode-medium
- DFS(深度优先遍历)
---

Given an integer array `nums` that may contain duplicates, return *all possible subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

```
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

<!-- more -->

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

 

**Constraints:**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`

# 分析

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/subsets-ii/
 * Runtime: 4 ms, faster than 71.30%
 * Memory Usage: 7.7 MB, less than 56.67%
 */
class Solution {
private:
    vector<int> nums;
    vector<vector<int>> res;
    vector<int> path;
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        this->nums = nums;
        dfs(0);
        return res;
    }
    void dfs(int start){
        res.push_back(path);
        for(int i = start; i < nums.size(); i++){
            if(i > start && nums[i] == nums[i-1]) continue;
            path.push_back(nums[i]);
            dfs(i+1);
            path.pop_back();
        }
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/subsets-ii/
 * Runtime: 84 ms, faster than 63.33%
 * Memory Usage: 40.9 MB, less than 80.00%
 */
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsetsWithDup = function(nums) {
    const res = [], path = [];
    function dfs(index){
        res.push([...path]);
        for(let i = index; i < nums.length; i++){
            if(i > index && nums[i] == nums[i-1]) continue;
            path.push(nums[i]);
            dfs(i+1);
            path.pop();
        }
    }
    nums.sort();
    dfs(0);    
    return res;
};
```

**java**

```c++
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/subsets-ii/
 * Beats : 76.26 %
 */
class Solution {
private:
    vector<vector<int>> res;
    vector<int> path;
    vector<int> nums;
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        this->nums = nums;
        dfs(0);
        return res;
    }
    void dfs(int index){
        res.push_back(path);
        for(int i = index; i < nums.size(); i++){
            if(i>index && nums[i] == nums[i-1]) continue;
            path.push_back(nums[i]);
            dfs(i + 1);
            path.pop_back();

        }
    }
};
```

