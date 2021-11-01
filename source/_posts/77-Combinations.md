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

 <!-- more -->

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

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/combinations/
 * Runtime: 28 ms, faster than 59.10%
 * Memory Usage: 10 MB, less than 48.81%
 */
class Solution {
private:
    vector<vector<int>> res;
    vector<int> path;
    int k, n;
public:
    vector<vector<int>> combine(int n, int k) {
        this->k = k;
        this->n = n;
        dfs(0,0);
        return res;
    }
    void dfs(int start, int level){
        if(level == k){
            res.push_back(path);
            return;
        }
        for(int i = start; i < n; i++){
            path.push_back(i+1);
            dfs(i+1,level+1);
            path.pop_back();
        }
    }
};
```

**javascript**

```javascript
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/combinations/
 * Runtime: 120 ms, faster than 76.42%
 * Memory Usage: 44.1 MB, less than 82.17%
 */
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function(n, k) {
    const res = [], path = [];
    function dfs(level, start){
        if(level === k){
            res.push([...path]);
            return;
        }
        for(let i = start; i < n; i++){
            path.push(i+1);
            dfs(level+1,i+1);
            path.pop();
        }
    }
    dfs(0,0);
    return res;
};
```

