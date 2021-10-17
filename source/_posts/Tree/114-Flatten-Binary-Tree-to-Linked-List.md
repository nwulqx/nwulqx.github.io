---
title: 114. Flatten Binary Tree to Linked List
date: 2021-10-17 16:35:12
tags:
- LeetCode-medium
- recursion(递归)
---

Given the `root` of a binary tree and an integer `targetSum`, return *all **root-to-leaf** paths where the sum of the node values in the path equals* `targetSum`*. Each path should be returned as a list of the node **values**, not node references*.

A **root-to-leaf** path is a path starting from the root and ending at any leaf node. A **leaf** is a node with no children.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg)

```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]
Explanation: There are two paths whose sum equals targetSum:
5 + 4 + 11 + 2 = 22
5 + 8 + 4 + 5 = 22
```

<!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```
Input: root = [1,2,3], targetSum = 5
Output: []
```

**Example 3:**

```
Input: root = [1,2], targetSum = 0
Output: []
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5000]`.
- `-1000 <= Node.val <= 1000`
- `-1000 <= targetSum <= 1000`

# 分析

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/flatten-binary-tree-to-linked-list/
 * Runtime: 92 ms, faster than 52.48% 
 * Memory Usage: 41.3 MB, less than 14.79%
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
 * @param {TreeNode} root
 * @return {void} Do not return anything, modify root in-place instead.
 */
var flatten = function(root) {
    let pre = null;
    function dfs(node){
        if(!node) return;
        dfs(node.right);
        dfs(node.left);
        node.right = pre;
        node.left = null;
        pre = node;
    }
    dfs(root);
    return root;
};
```



**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/flatten-binary-tree-to-linked-list/
 * Runtime: 4 ms, faster than 86.73% 
 * Memory Usage: 12.7 MB, less than 76.29%
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
private:
    TreeNode* pre = NULL;
public:
    void flatten(TreeNode* root) {
        if(root == NULL) return;
        flatten(root->right);
        flatten(root->left);
        root->right = pre;
        root->left = NULL;
        pre = root;
    }
};
```

