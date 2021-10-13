---
title: 120. Triangle
date: 2021-09-20 18:29:29
tags:
- LeetCode-easy
- DP(动态规划)
- Array
---

Given a `triangle` array, return *the minimum path sum from top to bottom*.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index `i` on the current row, you may move to either index `i` or index `i + 1` on the next row.

 <!-- more -->

**Example 1:**

```
Input: triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
Output: 11
Explanation: The triangle looks like:
   2
  3 4
 6 5 7
4 1 8 3
The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).
```

**Example 2:**

```
Input: triangle = [[-10]]
Output: -10
```

 

**Constraints:**

- `1 <= triangle.length <= 200`
- `triangle[0].length == 1`
- `triangle[i].length == triangle[i - 1].length + 1`
- `-104 <= triangle[i][j] <= 104`

 

**Follow up:** Could you do this using only `O(n)` extra space, where `n` is the total number of rows in the triangle?

# 分析

dp问题：https://leetcode.com/problems/triangle/discuss/38730/DP-Solution-for-Triangle

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/triangle/
 */
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        for(int i = triangle.size()-2; i >= 0; i--){
            for(int j = 0; j <= i; j++){
                triangle[i][j] += min(triangle[i+1][j],triangle[i+1][j+1]);
            }
        }
        return triangle[0][0];
    }
};
```

```js
/**
 * @param {number[][]} triangle
 * @return {number}
 */
var minimumTotal = function(triangle) {
    let m = triangle.length;
    for(let i = m-2; i >= 0; i--){
        for(let j = 0; j <= i; j++){
            triangle[i][j] += Math.min(triangle[i+1][j],triangle[i+1][j+1]);
        }
    }
    return triangle[0][0];
};
```

