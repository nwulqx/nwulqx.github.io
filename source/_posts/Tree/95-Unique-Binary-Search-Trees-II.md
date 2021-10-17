---
title: 95. Unique Binary Search Trees II
date: 2021-10-12 22:29:37
tags:
- LeetCode-medium
- recursion(递归)
- Tree
---

Given an integer `n`, return *all the structurally unique **BST'**s (binary search trees), which has exactly* `n` *nodes of unique values from* `1` *to* `n`. Return the answer in **any order**.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

```
Input: n = 3
Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]
```

**Example 2:**

```
Input: n = 1
Output: [[1]]
```

 <!-- more -->

**Constraints:**

- `1 <= n <= 8`

# 分析

递归解法

**javascript**

```javascript
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/unique-binary-search-trees-ii/
 * Runtime: 104 ms, faster than 66.51% 
 * Memory Usage: 45.5 MB, less than 58.80%
 */
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {number} n
 * @return {TreeNode[]}
 */
var generateTrees = function(n) {
    var dfs = function(start, end){
        const res = [];
        if(start > end){
            res.push(null);
            return res;
        }
        for(let i = start; i <= end; i++){
            const leftList = dfs(start, i - 1);
            const rightList = dfs(i + 1, end);
            for(const left of leftList){
                for(const right of rightList){
                    const root = new TreeNode(i+1);
                    root.left = left;
                    root.right = right;
                    res.push(root);
                }
            }
        }
        return res;
    }
    return dfs(0, n - 1);
};
```

**c++**

```c++
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/unique-binary-search-trees-ii/
 * Runtime: 14 ms, faster than 87.65 %
 * Memory Usage: 16.1 MB, less than 49.20 %
 */
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<TreeNode*> generateTrees(int n) {
        return dfs(0,n-1);
    }
    vector<TreeNode*> dfs(int start, int end){
        vector<TreeNode*> res;
        if(start > end){
            res.push_back(NULL);
            return res;
        };
        
        for(int i = start; i <= end; i++){
            vector<TreeNode*> leftList = dfs(start, i - 1);
            vector<TreeNode*> rightList = dfs(i + 1, end);
            for(TreeNode* left : leftList){
                for(TreeNode* right : rightList){
                    TreeNode* root = new TreeNode(i+1);
                    root->left = left;
                    root->right = right;
                    res.push_back(root);
                }
            }
        }
        return res;
    }
};
```

# 总结

关键点在于for循环的递归理解~