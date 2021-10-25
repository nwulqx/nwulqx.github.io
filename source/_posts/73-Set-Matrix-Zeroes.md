---
title: 73. Set Matrix Zeroes
date: 2021-09-20 12:56:59
tags:
- Array
- LeetCode-medium
- matrix(矩阵)
---

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s, and return *the matrix*.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

 <!-- more -->

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

```
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

 

**Constraints:**

- `m == matrix.length`
- `n == matrix[0].length`
- `1 <= m, n <= 200`
- `-231 <= matrix[i][j] <= 231 - 1`

 

**Follow up:**

- A straightforward solution using `O(mn)` space is probably a bad idea.
- A simple improvement uses `O(m + n)` space, but still not the best solution.
- Could you devise a constant space solution?

# 分析

参考：https://leetcode.com/problems/set-matrix-zeroes/solution/

https://leetcode.com/problems/set-matrix-zeroes/discuss/26014/Any-shorter-O(1)-space-solution

- 利用行列头存储当前行列的状态

- 设置一个bool值，用于列头的判断，因为列头本身作为判断标准，需要单独判断

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/set-matrix-zeroes/
 * Runtime: 4 ms Beats : 80 %
 * Memory: 7.5 MB Beats:  80 %
 */
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        bool isCol = false;
        for(int i = 0; i < m; i++){
            if(matrix[i][0] == 0) isCol = true;
            for(int j = 1; j < n; j++){
                if(matrix[i][j] == 0){
                    matrix[i][0] = matrix[0][j] = 0;
                }
            }
        }
        for(int i = m-1; i >= 0; i--){
            for(int j = 1; j < n; j++){
                if(matrix[i][0] == 0 || matrix[0][j] == 0){
                    matrix[i][j] = 0;
                }
            }
            if(isCol) matrix[i][0] = 0;
        }
    }
};
```

**javascript**

```javascript
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/set-matrix-zeroes/
 * Runtime: 137 ms, faster than 30.24%
 * Memory Usage: 41 MB, less than 76.36%
 */
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var setZeroes = function(matrix) {
    const m = matrix.length, n = matrix[0].length;
    let isCol = false;
    for(let i = 0; i < m; i++){
        if(matrix[i][0] === 0) isCol = true;
        for(let j = 1; j < n; j++){
            if(matrix[i][j] === 0){
                matrix[i][0] = matrix[0][j] = 0;
            }
        }
    }
    for(let i = m-1; i >= 0; i--){
        for(let j = 1; j < n; j++){
            if(matrix[i][0] === 0 || matrix[0][j] === 0){
                matrix[i][j] = 0;
            }
        }
        if(isCol) matrix[i][0] = 0;
    }
};
```

