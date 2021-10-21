---
title: 54. Spiral Matrix
date: 2021-10-21 22:42:09
tags:
- Array
- 螺旋矩阵
- LeetCode-medium
---

Given an `m x n` `matrix`, return *all elements of the* `matrix` *in spiral order*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

<!--more-->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

 

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 10`
- `-100 <= matrix[i][j] <= 100`

# Analysis

**c++**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/spiral-matrix/
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 6.7 MB, less than 99.82%
 */
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> res;
        int m = matrix.size() - 1;
        int n = matrix[0].size() - 1;
        for(int x=0, y=0;x<=m&&y<=n;x++,y++,m--,n--){
            for(int j = y;j <= n; j++){
                res.push_back(matrix[x][j]);
            }
            for(int i = x+1; i <= m; i++){
                res.push_back(matrix[i][n]);
            }
            // x == m 只有一列不需要输出
            for(int j = n-1; j >= y && x != m;j--){
                res.push_back(matrix[m][j]);
            }
            // y == n 只有一行不需要输出
            for(int i = m-1; i > x && y!= n;i--){
                res.push_back(matrix[i][y]);
            }
        }
        return res;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/spiral-matrix/
 * Runtime: 95 ms, faster than 34.13%
 * Memory Usage: 38.4 MB, less than 67.02%
 */
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function(matrix) {
    const res = [];
    let m = matrix.length - 1, n = matrix[0].length - 1;
    for(let x = 0, y = 0; x <= m && y <= n; x++,y++,m--,n--){
        for(let j = y; j <= n; j++){
            res.push(matrix[x][j]);
        }
        for(let i = x+1; i <= m; i++){
            res.push(matrix[i][n]);
        }
        // x == m 只有一列不需要输出
        for(let j = n-1; j >= y && x != m; j--){
            res.push(matrix[m][j]);
        }
        // y == n 只有一行不需要输出
        for(let i = m-1; i > x && y != n; i--){
            res.push(matrix[i][y]);
        }
    }
    return res;
};
```

