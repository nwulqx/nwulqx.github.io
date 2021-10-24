---
title: 64. Minimum Path Sum
date: 2021-09-12 19:47:10
tags:
- DP(动态规划)
- Array
---

Given a `m x n` `grid` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

```
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
```

  <!--more-->

**Example 2:**

```
Input: grid = [[1,2,3],[4,5,6]]
Output: 12
```

 

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 200`
- `0 <= grid[i][j] <= 100`

# 分析

参考：https://leetcode.com/problems/minimum-path-sum/discuss/23457/C%2B%2B-DP

**c++**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/minimum-path-sum/
 * Runtime: 11 ms, faster than 50.53%
 * Memory Usage: 9.6 MB, less than 86.47%
 */
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        for(int i = 1; i < m; i++){
            grid[i][0] += grid[i-1][0];
        }
        for(int j = 1; j <n; j++){
            grid[0][j] += grid[0][j-1];
        }
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                grid[i][j] += min(grid[i-1][j],grid[i][j-1]);
            }
        }
        return grid[m-1][n-1];
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/minimum-path-sum/
 * Runtime: 103 ms, faster than 43.03%
 * Memory Usage: 40.4 MB, less than 86.55%
 */
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function(grid) {
    const m = grid.length, n = grid[0].length;
    for(let i = 1; i < m; i++){
        grid[i][0] += grid[i-1][0];
    }
    for(let j = 1; j < n; j++){
        grid[0][j] += grid[0][j-1];
    }
    for(let i = 1; i < m; i++){
        for(let j = 1; j < n; j++){
            grid[i][j] += Math.min(grid[i-1][j], grid[i][j-1]);
        }
    }
    return grid[m-1][n-1];
};
```

