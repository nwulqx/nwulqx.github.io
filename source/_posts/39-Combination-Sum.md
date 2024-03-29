---
title: 39. Combination Sum
date: 2021-10-20 22:45:19
tags:
- Array
- LeetCode-medium
- DFS(深度优先遍历)
---

Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all **unique combinations** of* `candidates` *where the chosen numbers sum to* `target`*.* You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

 

**Example 1:**

```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```

 <!-- more -->

**Example 2:**

```
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```

**Example 3:**

```
Input: candidates = [2], target = 1
Output: []
```

**Example 4:**

```
Input: candidates = [1], target = 1
Output: [[1]]
```

**Example 5:**

```
Input: candidates = [1], target = 2
Output: [[1,1]]
```

 

**Constraints:**

- `1 <= candidates.length <= 30`
- `1 <= candidates[i] <= 200`
- All elements of `candidates` are **distinct**.
- `1 <= target <= 500`

# Analysis

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/combination-sum/
 * Runtime: 152 ms, faster than 24.43%
 * Memory Usage: 41.3 MB, less than 68.95%
 */
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function(candidates, target) {
    const path = [];
    const res = [];
    function dfs(start, sum){
        if(sum > target) return;
        if(sum === target){
            res.push([...path]);
            return;
        }
        for(let i = start; i < candidates.length; i++){
            path.push(candidates[i]);
            dfs(i, sum+candidates[i]);
            path.pop();
        }
    }
    dfs(0,0);
    return res;
};
```

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/combination-sum/
 * Runtime: 11 ms, faster than 53.48%
 * Memory Usage: 11 MB, less than 54.20%
 */
class Solution {
private:
    int target;
    vector<int> path;
    vector<vector<int>> res;
    vector<int> candidates;
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        this->target = target;
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
            path.push_back(candidates[i]);
            dfs(i, sum+candidates[i]);
            path.pop_back();
        }
    }
};
```

