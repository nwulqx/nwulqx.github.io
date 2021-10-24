---
title: 63. Unique Paths II
date: 2021-09-12 19:33:50
tags:
- DP(动态规划)
- Array
---

A robot is located at the top-left corner of a `m x n` grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and space is marked as `1` and `0` respectively in the grid.

 <!--more-->

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg)

```
Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
Explanation: There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg)

```
Input: obstacleGrid = [[0,1],[0,0]]
Output: 1
```

 

**Constraints:**

- `m == obstacleGrid.length`
- `n == obstacleGrid[i].length`
- `1 <= m, n <= 100`
- `obstacleGrid[i][j]` is `0` or `1`.



# 分析

参考：https://leetcode.com/problems/unique-paths-ii/solution/

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/unique-paths-ii/
 * Runtime: 4 ms Beats : 65.28 %
 * Memory: 7.5 MB Beats:  84.12 %
 */
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        if(obstacleGrid[0][0] == 1){
            return 0;
        }
        obstacleGrid[0][0] = 1;
        for(int i = 1; i < n; i++){
            obstacleGrid[0][i] = (obstacleGrid[0][i]==0 && obstacleGrid[0][i-1]==1)?1:0;
        }
        for(int i = 1; i < m; i++){
            obstacleGrid[i][0] = (obstacleGrid[i][0]==0 && obstacleGrid[i-1][0]==1)?1:0;
        }
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                if(obstacleGrid[i][j] == 0){
                    obstacleGrid[i][j] = obstacleGrid[i-1][j] + obstacleGrid[i][j-1];
                }else {
                    obstacleGrid[i][j] = 0;
                }
            }
        }
        return obstacleGrid[m-1][n-1];
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/unique-paths-ii/
 * Runtime: 139 ms Beats : 13.56 %
 * Memory: 38.8 MB Beats:  92.50 % 
 */
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function(obstacleGrid) {
    var m = obstacleGrid.length, n = obstacleGrid[0].length;
    if(obstacleGrid[0][0] === 1) return 0;
    obstacleGrid[0][0] = 1;
    for(let i = 1; i < m; i++){
        obstacleGrid[i][0] = (obstacleGrid[i][0] === 0 && obstacleGrid[i-1][0] === 1)?1:0;
    }
    for(let i = 1; i < n; i++){
        obstacleGrid[0][i] = (obstacleGrid[0][i] === 0 && obstacleGrid[0][i-1] === 1)?1:0;
    }
    for(let i = 1; i < m; i++){
        for(let j = 1; j < n; j++){
            if(obstacleGrid[i][j] === 0){
                obstacleGrid[i][j] = obstacleGrid[i-1][j] + obstacleGrid[i][j-1];
            }else{
                obstacleGrid[i][j] = 0;
            }
        }
    }
    return obstacleGrid[m-1][n-1];
};
```

