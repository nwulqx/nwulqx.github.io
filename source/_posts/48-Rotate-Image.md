---
title: 48. Rotate Image
date: 2021-10-21 21:09:04
tags:
- Array
- LeetCode-medium
---

You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).

You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]
```

 <!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg)

```
Input: matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
Output: [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]
```

**Example 3:**

```
Input: matrix = [[1]]
Output: [[1]]
```

**Example 4:**

```
Input: matrix = [[1,2],[3,4]]
Output: [[3,1],[4,2]]
```

 

**Constraints:**

- `matrix.length == n`
- `matrix[i].length == n`
- `1 <= n <= 20`
- `-1000 <= matrix[i][j] <= 1000`

# Analysis

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/rotate-image/
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 7.1 MB, less than 32.75%
 */
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        reverse(matrix.begin(),matrix.end());
        for(int i = 0; i < matrix.size(); i++){
            // 重点在于j = i+1
            for(int j = i+1; j < matrix[0].size(); j++){
                swap(matrix[i][j],matrix[j][i]);
            }
        }
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/rotate-image/
 * Runtime: 93 ms, faster than 35.22% 
 * Memory Usage: 38.7 MB, less than 75.59%
 */
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var rotate = function(matrix) {
    matrix.reverse();
    for(let i = 0; i < matrix.length; i++){
        for(let j = i+1; j < matrix[0].length; j++){
            const temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }
};
```

