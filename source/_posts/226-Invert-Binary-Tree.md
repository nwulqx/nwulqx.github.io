---
title: 226. Invert Binary Tree
date: 2021-10-17 21:58:24
tags:
- LeetCode-easy
- recursion(递归)
---

Given the `root` of a binary tree, invert the tree, and return *its root*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg)

```
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
```

 <!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg)

```
Input: root = [2,1,3]
Output: [2,3,1]
```

**Example 3:**

```
Input: root = []
Output: []
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

# Analysis

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/invert-binary-tree/
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 9.8 MB, less than 36.90%
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
    TreeNode* invertTree(TreeNode* root) {
        if(!root) return root;
        TreeNode* tmp = root->left;
        root->left = root->right;
        root->right = tmp;
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/invert-binary-tree/
 * Runtime: 76 ms, faster than 68.80%
 * Memory Usage: 40.1 MB, less than 29.83%
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
 * @return {TreeNode}
 */
var invertTree = function(root) {
    if(!root) return root;
    const tmp = root.left;
    root.left = root.right;
    root.right = tmp;
    invertTree(root.left);
    invertTree(root.right);
    return root;
};
```

