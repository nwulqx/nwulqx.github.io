---
title: 77. Combinations
date: 2021-09-20 16:49:51
tags:
- Array
- LeetCode-medium
- DFS(深度优先遍历)
---

Given two integers `n` and `k`, return *all possible combinations of* `k` *numbers out of the range* `[1, n]`.

You may return the answer in **any order**.

​    <!-- more -->

**Example 1:**

```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

**Example 2:**

```
Input: n = 1, k = 1
Output: [[1]]
```

 

**Constraints:**

- `1 <= n <= 20`
- `1 <= k <= n`

# 分析

DFS遍历

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/combinations/
 */
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;
        vector<int> path;
        dfs(res,path,1,n,k);
        return res;
    }
    void dfs(vector<vector<int>> &res,vector<int> &path, int index,int n, int k){
        if(path.size() == k){
            res.push_back(path);
            return;
        }
        for(int i = index; i <=n; i++){
            path.push_back(i);
            dfs(res, path, i+1,n,k);
            path.pop_back();
        }
    }
};
```

```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function(n, k) {
    const res = [],path = [];
    function dfs(index,cnt){
        if(cnt === k) res.push([...path]);
        for(let i = index; i < n; i++){
            path.push(i+1);
            dfs(i+1,cnt+1);
            path.pop();
        }
    }
    dfs(0,0);
    return res;
};
```

