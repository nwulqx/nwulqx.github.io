---
title: 59. Spiral Matrix II
date: 2021-09-12 16:56:45
tags:
- LeetCode-medium
- Array
- 螺旋矩阵
---

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```c++
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

**Example 2:**

```c++
Input: n = 1
Output: [[1]]
```

 

**Constraints:**

- `1 <= n <= 20`

<!--more-->

# 分析

这个题目在pat中也遇到过，pat的边界条件更好，在二次循环得过程中，对于元素的边界判断也应该加上`i < length`，防止在循环`边`的时候出现边界问题。

类似题目：https://pintia.cn/problem-sets/994805342720868352/problems/994805363117768704

**JavaScript版本**

**js建立二维数组**：`var res = [...Array(n)].map(() => Array(n).fill(0));`

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/spiral-matrix-ii/
 * Runtime: 90 ms, faster than 41.03%
 * Memory Usage: 38.8 MB, less than 62.24%
 */
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
    let k = 1 , level = 0;
    const res = [...Array(n)].map(item => Array(n));
    while(k <= n*n){
        for(let j = level; j < n-level && k <= n*n; j++){
            res[level][j] = k++;
        }
        for(let i = level+1;i < n-level && k <= n*n; i++){
            res[i][n-level-1] = k++;
        }
        for(let j = n-level-2; j >= level && k <= n*n; j--){
            res[n-level-1][j] = k++;
        }
        for(let i = n-level-2; i > level && k <= n*n; i--){
            res[i][level] = k++;
        }
        level++;
    }
    return res;
};
```

**c++**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/spiral-matrix-ii/
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 6.6 MB, less than 17.38%
 */
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res(n, vector<int>(n));
        int k = 1 , index = 0;
        while(k <= n*n){
            for(int j = index; j < n-index && k <= n*n;j++){
                res[index][j] = k++;
            }
            for(int i = index+1; i < n-index && k <= n*n; i++){
                res[i][n-1-index] = k++;
            }
            for(int j = n-index-2; j >= index && k <= n*n; j--){
                res[n-index-1][j] = k++;
            }
            for(int i = n-index-2; i > index && k <= n*n;i--){
                res[i][index] = k++;
            }
            index++;
        }
        return res;
    }
};
```

**java**

```c++
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/spiral-matrix-ii/
 * Runtime: 0 ms Beats : 100%
 * Memory: 6.5 MB Beats:  87.36% 
 */
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res(n, vector<int>(n));
        int k = 1, i = 0;
        while(k <= n*n){
            int j = i;
            while(j < n-i && k <= n*n){
                res[i][j++] = k++;
            }
            j = i + 1;
            while(j < n-i && k <= n*n){
                res[j++][n-i-1] = k++;
            }
            j = n-i-2;
            while(j >= i && k <= n*n){
                res[n-i-1][j--] = k++;
            }
            j = n-2-i;
            while(j > i && k <= n*n){
                res[j--][i] = k++;
            }
            i++;
        }
        return res;
    }
};
```
