---
title: 235. Lowest Common Ancestor of a Binary Search Tree
date: 2021-10-17 23:18:16
tags:
- LeetCode-easy
- recursion(递归)
- LCA(最近公共祖先)
---

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
```

 <!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.
```

**Example 3:**

```
Input: root = [2,1], p = 2, q = 1
Output: 2
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[2, 105]`.
- `-109 <= Node.val <= 109`
- All `Node.val` are **unique**.
- `p != q`
- `p` and `q` will exist in the BST.

# Analysis

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/
 * Runtime: 32 ms, faster than 59.21% 
 * Memory Usage: 23.3 MB, less than 11.59%
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
        if(root->val == p->val || root->val == q->val) return root;
        if(root->val < p->val && root->val < q->val) return lowestCommonAncestor(root->right, p,q);
        if(root->val > p->val && root->val > q->val) return lowestCommonAncestor(root->left, p,q);
        return root;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/
 * Runtime: 96 ms, faster than 74.15%
 * Memory Usage: 49.2 MB, less than 13.15%
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
    if(root.val > p.val && root.val > q.val) return lowestCommonAncestor(root.left,p,q);
    if(root.val < p.val && root.val < q.val) return lowestCommonAncestor(root.right,p,q);
    return root;
};
```

