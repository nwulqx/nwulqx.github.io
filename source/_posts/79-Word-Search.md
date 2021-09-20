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

​      <!-- more -->

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

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

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/word-search/
 */
class Solution {
private:
    vector<vector<char>> board;
    string word;
    vector<vector<bool>> visit;
    bool res = false;
    int dir[4][2] = {{1,0},{0,1},{0,-1},{-1,0}};
    int m,n;
public:
    bool exist(vector<vector<char>>& board, string word) {
        this -> board = board;
        this -> word = word;
        m = board.size(), n = board[0].size();
        visit.resize(m, vector<bool>(n));
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(word[0] == board[i][j]){
                    visit[i][j] = true;
                    dfs(i, j, 0);
                    visit[i][j] = false;
                }
            }
        }
        return res;
    }
    void dfs(int x, int y, int index){
        if(res) return;
        if(index == word.size()-1){
            res = true;
            return;
        }
        for(int i = 0; i < 4; i++){
            int tx = x+dir[i][0],ty = y+dir[i][1];
            if(tx >= 0 && tx < m && ty >= 0 && ty < n && word[index + 1] == board[tx][ty] &&!visit[tx][ty]) {
                visit[tx][ty] = true;
                dfs(tx, ty, index + 1);
                visit[tx][ty] = false;
            }
        }
    }
};
```

```javascript
/**
 * @param {character[][]} board
 * @param {string} word
 * @return {boolean}
 */
var exist = function(board, word) {
    const dir = [[0,1],[0,-1],[1,0],[-1,0]];
    let res = false;
    const m = board.length, n = board[0].length;
    const visit = [...Array(m)].map(()=> Array(n).fill(false));
    function dfs(x,y,index){
        if(res) return;
        if(index === word.length-1 && board[x][y] === word[index]){
            res = true;
            return;
        }
        for(let i = 0; i < 4; i++){
            const tx = x + dir[i][0];
            const ty = y + dir[i][1];
            if(tx >= 0 && tx < m && ty >= 0 && ty < n && !visit[tx][ty] && board[x][y] === word[index]){
                visit[tx][ty] = true;
                dfs(tx,ty,index+1);
                visit[tx][ty] = false;
            }
        }
    }
    for(let i = 0; i < m; i++){
        for(let j = 0; j < n;j++){
            visit[i][j] = true;
            dfs(i,j,0);
            visit[i][j] = false;
        }
    }
    return res;
};
```

