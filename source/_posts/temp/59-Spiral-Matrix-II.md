---
title: 59. Spiral Matrix II
date: 2021-09-12 16:56:45
tags:
- LeetCode-medium
- Array
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



**JavaScript版本**

**js建立二维数组**：`var res = [...Array(n)].map(() => Array(n).fill(0));`

```js
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
    var i = 0, k = 1, len = n*n;
    var res = [...Array(n)].map(() => Array(n).fill(0));
    while(k <= len){
        var temp = [];
        var j = i;
        while(j < n - i && k <= len){
            res[i][j++] = k++;
        }
        j = i + 1;
        while(j < n-i && k <= len){
            res[j++][n-i-1] = k++;
        }
        j = n-2-i;
        while(j > i && k <= len){
            res[n-i-1][j--] = k++;
        }
        j = n-1-i;
        while(j > i && k <= len){
            res[j--][i] = k++;
        }
        i++;
    }
    return res;
};
```

