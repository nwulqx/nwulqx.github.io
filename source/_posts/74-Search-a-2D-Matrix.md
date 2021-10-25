---
title: 74. Search a 2D Matrix
date: 2021-09-20 13:32:22
tags:
- Array
- LeetCode-medium
---

Write an efficient algorithm that searches for a value in an `m x n` matrix. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.



**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

<!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```

 

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 100`
- `-104 <= matrix[i][j], target <= 104`



# 分析

二维数组的二分法

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/search-a-2d-matrix/
 * Runtime: 68 ms, faster than 93.93%
 * Memory Usage: 40 MB, less than 20.22%
 */
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var searchMatrix = function(matrix, target) {
    const m = matrix.length, n = matrix[0].length;
    let low = 0, high = m*n-1;
    while(low <= high){
        const mid = Math.trunc(low + (high-low)/2);
        const x = Math.trunc(mid / n), y = mid % n;
        if(matrix[x][y] === target) return true;
        if(matrix[x][y] < target) low = mid + 1;
        else high = mid - 1;
    }
    return false;
};
```

**c++**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/search-a-2d-matrix/
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 9.4 MB, less than 79.04%
 */
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int low = 0, m = matrix.size(), n = matrix[0].size(), high = m*n-1;
        while(low <= high){
            int mid = low + (high - low)/2;
            int x = mid / n, y = mid % n;
            if(matrix[x][y] == target) return true;
            if(matrix[x][y] > target) high = mid - 1;
            else low = mid + 1;
        }
        return false;
    }
};
```

