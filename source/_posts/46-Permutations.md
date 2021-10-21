---
title: 46. Permutations
date: 2021-10-21 21:07:12
tags:
- Array
- LeetCode-medium
- DFS(深度优先遍历)
- DFS去重
---

Given an array `nums` of distinct integers, return *all the possible permutations*. You can return the answer in **any order**.

 

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

 <!-- more -->

**Example 2:**

```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

**Example 3:**

```
Input: nums = [1]
Output: [[1]]
```

 

**Constraints:**

- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- All the integers of `nums` are **unique**.

# Analysis

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/permutations/
 * Runtime: 137 ms, faster than 25.70%
 * Memory Usage: 42.3 MB, less than 34.75%
 */
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function(nums) {
    const path = [];
    const res = [];
    const st = new Set();
    function dfs(level){
        if(level === nums.length){
            res.push([...path]);
            return;
        }
        for(let i = 0; i < nums.length; i++){
            if(st.has(nums[i])) continue;
            st.add(nums[i]);
            path.push(nums[i]);
            dfs(level+1);
            path.pop();
            st.delete(nums[i]);
        }
    }
    dfs(0);
    return res;
};
```

**c++**

```c++
/*
 * app:leetcode lang: c++
 *https://leetcode.com/problems/permutations/
 * Runtime: 7 ms, faster than 24.51%
 * Memory Usage: 8.3 MB, less than 17.72%
 */
class Solution {
private:
    unordered_set<int> st;
    vector<int> nums;
    vector<int> path;
    vector<vector<int>> res;
public:
    vector<vector<int>> permute(vector<int>& nums) {
        this->nums = nums;
        dfs(0);
        return res;
    }
    void dfs(int level){
        if(level == nums.size()){
            res.push_back(path);
            return;
        }
        for(int i = 0; i < nums.size(); i++){
            if(st.find(nums[i]) != st.end()) continue;
            st.insert(nums[i]);
            path.push_back(nums[i]);
            dfs(level+1);
            st.erase(nums[i]);
            path.pop_back();
        }
    }
};
```

