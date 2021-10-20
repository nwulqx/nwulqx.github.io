---
title: 40. Combination Sum II
date: 2021-10-20 22:46:40
tags:
- Array
- LeetCode-medium
- DFS(深度优先遍历)
- DFS去重
---

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

 

**Example 1:**

```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

 <!-- more -->

**Example 2:**

```
Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]
```

 

**Constraints:**

- `1 <= candidates.length <= 100`
- `1 <= candidates[i] <= 50`
- `1 <= target <= 30`

# Analysis

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/combination-sum-ii/
 * Runtime: 156 ms, faster than 13.85% 
 * Memory Usage: 40.9 MB, less than 37.74% 
 */
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum2 = function(candidates, target) {
    const res = [];
    const path = [];
    function dfs(start, sum){
        if(sum > target) return;
        if(sum === target){
            res.push([...path]);
            return;
        }
        for(let i = start; i < candidates.length; i++){
            if(i > start && candidates[i] === candidates[i-1]) continue;
            path.push(candidates[i]);
            dfs(i+1, sum+candidates[i]);
            path.pop();
        }
    }
    candidates.sort((a,b)=>a-b);
    dfs(0,0);
    return res;
};
```

**c++**

```c++
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/combination-sum-ii/
 * Runtime: 12 ms, faster than 33.76%
 * Memory Usage: 10.6 MB, less than 88.24% 
 */
class Solution {
private:
    int target;
    vector<int> path;
    vector<vector<int>> res;
    vector<int> candidates;
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        this->target = target;
        sort(candidates.begin(),candidates.end());
        this->candidates = candidates;
        dfs(0, 0);
        return res;
    }
    void dfs(int start, int sum){
        if(sum > target) return;
        if(sum == target){
            res.push_back(path);
            return;
        }
        for(int i = start; i < candidates.size(); i++){
            if(i > start && candidates[i] == candidates[i-1]) continue;
            path.push_back(candidates[i]);
            dfs(i+1, sum+candidates[i]);
            path.pop_back();
        }
    }
};
```

