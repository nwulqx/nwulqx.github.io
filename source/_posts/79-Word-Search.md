---
title: 79. Word Search
date: 2021-09-20 17:19:31
tags:
- Array
- LeetCode-medium
- DFS(深度优先遍历)
---

Given an `m x n` grid of characters `board` and a string `word`, return `true` *if* `word` *exists in the grid*.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

<!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```

**Example 3:**

![img](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
```

 

**Constraints:**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` and `word` consists of only lowercase and uppercase English letters.

 

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

# 分析

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/word-search/
 * Runtime: 204 ms, faster than 82.73%
 * Memory Usage: 7.9 MB, less than 7.46% 
 */
class Solution {
private:
    int m,n;
    string word;
    vector<vector<char>> board;
    vector<vector<bool>> visit;
    int direct[4][2] = {{0,1},{0,-1},{1,0},{-1,0}};
    bool res = false;
public:
    bool exist(vector<vector<char>>& board, string word) {
        this->word = word;
        this->m = board.size();
        this->n = board[0].size();
        this->board = board;
        visit.resize(m,vector<bool>(n,false));
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(board[i][j] == word[0]){
                    visit[i][j] = true;
                    dfs(0,i,j);
                    visit[i][j] = false;
                }
            }
        }
        return res;
    }
    void dfs(int level, int x, int y){
        if(res) return;
        if(level == word.size()-1){
            res = true;
            return;
        }
        for(int i = 0; i < 4; i++){
            int tx = x + direct[i][0];
            int ty = y + direct[i][1];
            if(tx >= 0 && tx < m && ty >=0 && ty < n && word[level+1] == board[tx][ty] && !visit[tx][ty]){
                visit[tx][ty] = true;
                dfs(level+1,tx,ty);
                visit[tx][ty] = false;
            }
        }
    }
};
```
**javascript**

js真tm是个垃圾语言，lenght拼写错误，竟然不报错

```javascript
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/word-search/
 * Runtime: 288 ms, faster than 87.77%
 * Memory Usage: 39.8 MB, less than 57.18%
 */
/**
 * @param {character[][]} board
 * @param {string} word
 * @return {boolean}
 */
var exist = function(board, word) {
    const m = board.length, n = board[0].length;
    const visit = [...Array(m)].map(item => Array(n).fill(false));
    let res = false;
    const direct = [[0,1],[0,-1],[1,0],[-1,0]];
    function dfs(level,x,y){
        if(res) return;
        if(level === word.length-1){
            res = true;
            return;
        }
        for(let i = 0; i < 4; i++){
            const tx = x + direct[i][0];
            const ty = y + direct[i][1];
            if(tx>=0 && tx < m && ty>=0 && ty <n && !visit[tx][ty]&& board[tx][ty]===word[level+1] ){
                visit[tx][ty] = true;
                dfs(level+1,tx,ty);
                visit[tx][ty] = false;
            }
        }
    }
    for(let i = 0; i < m; i++){
        for(let j = 0; j < n; j++){
            if(board[i][j]===word[0]){
                visit[i][j] = true;
                dfs(0,i,j);
                visit[i][j] = false;
            }
        }
    }
    return res;
};
```

