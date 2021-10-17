---
title: 236. Lowest Common Ancestor of a Binary Tree
date: 2021-10-17 23:18:29
tags:
- LeetCode-medium
- recursion(递归)
- LCA(最近公共祖先)
---

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

 <!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

**Example 3:**

```
Input: root = [1,2], p = 1, q = 2
Output: 1
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[2, 105]`.
- `-109 <= Node.val <= 109`
- All `Node.val` are **unique**.
- `p != q`
- `p` and `q` will exist in the tree.

# Analysis

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/
 * Runtime: 16 ms, faster than 74.73 % 
 * Memory Usage: 14.3 MB, less than 59.43 %
 */
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root) return root;
        if(p->val == root->val || q->val == root->val) return root;
        TreeNode* left = lowestCommonAncestor(root->left,p,q);
        TreeNode* right = lowestCommonAncestor(root->right,p,q);
        if(left && right) return root;
        return left != NULL?left:right;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/
 * Runtime: 88 ms, faster than 87.26%
 * Memory Usage: 48.7 MB, less than 26.02%
 */
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */
var lowestCommonAncestor = function(root, p, q) {
    if(!root) return root;
    if(root.val === p.val || root.val === q.val) return root;
    const left = lowestCommonAncestor(root.left, p,q);
    const right = lowestCommonAncestor(root.right, p,q);
    if(left && right) return root;
    return left?left:right;
};
```

