---
title: 36. Valid Sudoku
date: 2021-10-19 23:44:34
tags:
- Array
- LeetCode-medium
- 数独(Sudoku)
---

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

 

**Example 1:**

![img](./36-Valid-Sudoku.png)

```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

 <!-- more -->

**Example 2:**

```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

 

**Constraints:**

- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `1-9` or `'.'`.

# Analysis

**javascirpt**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/valid-sudoku/
 * Runtime: 127 ms, faster than 31.39%
 * Memory Usage: 44.3 MB, less than 16.69%
 */
/**
 * @param {character[][]} board
 * @return {boolean}
 */
var isValidSudoku = function(board) {
    const used1 = [...Array(9)].map(item => Array(9).fill(0));
    const used2 = [...Array(9)].map(item => Array(9).fill(0));
    const used3 = [...Array(9)].map(item => Array(9).fill(0));
    for(let i = 0; i < board.length; i++){
        for(let j = 0; j < board[0].length; j++){
            if(board[i][j] !== '.'){
                const k = Math.trunc(i/3)*3 + Math.trunc(j/3);
                const num = board[i][j] - '0' - 1;
                if(used1[i][num] || used2[j][num] || used3[k][num]){
                    return false;
                }
                used1[i][num] = used2[j][num] = used3[k][num] = 1;
            }
        }
    }
    return true;
};
```



**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/valid-sudoku/
 * Runtime: 24 ms, faster than 55.88%
 * Memory Usage: 18.1 MB, less than 72.18% 
 */
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int used1[9][9] = {0},used2[9][9] = {0},used3[9][9] = {0};
        for(int i = 0; i < board.size(); i++){
            for(int j = 0; j < board[0].size(); j++){
                if(board[i][j] != '.'){
                    int nums = board[i][j] - '0' - 1;
                    int k = i/3*3 + j/3;
                    if(used1[i][nums] || used2[j][nums] || used3[k][nums]){
                        return false;
                    }
                    used1[i][nums] = used2[j][nums] = used3[k][nums] = 1;
                }
            }
        }
        return true;
    }
};
```

