---
title: 106. Construct Binary Tree from Inorder and Postorder Traversal
date: 2021-10-13 23:20:27
tags:
- LeetCode-easy
- Tree(树)
- recursion(递归)
- In-Order Traversal(中序遍历)
---

Given two integer arrays `inorder` and `postorder` where `inorder` is the inorder traversal of a binary tree and `postorder` is the postorder traversal of the same tree, construct and return *the binary tree*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
Output: [3,9,20,null,null,15,7]
```

<!-- more -->

**Example 2:**

```
Input: inorder = [-1], postorder = [-1]
Output: [-1]
```

 

# 分析

**javascript**

```js
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
 * Runtime: 181 ms, faster than 21.80%
 * Memory Usage: 41.8 MB, less than 88.31%
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
 * @param {number[]} inorder
 * @param {number[]} postorder
 * @return {TreeNode}
 */
var buildTree = function(inorder, postorder) {
    function helper(postL, postR, inL, inR){
        if(postL > postR || inL > inR) return null;
        const root = new TreeNode();
        root.val = postorder[postR];
        let k = inL;
        while(k!==inR && inorder[k]!==postorder[postR]){
            k++;
        }
        const numL = k-inL;
        root.left = helper(postL,postL+numL-1,inL,k-1);
        root.right = helper(postL+numL,postR-1,k+1,inR);
        return root;
    }
    const n = postorder.length;
    const m = inorder.length;
    return helper(0,n-1,0,m-1);
};
```

**c++**

```c++
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
 * Runtime: 59 ms, faster than 12.48%
 * Memory Usage: 26.1 MB, less than 68.23%
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
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        int n = postorder.size();
        int m = inorder.size();
        return helper(0,n-1,0,m-1,inorder,postorder);
    }
    TreeNode* helper(int postL, int postR, int inL, int inR, vector<int>& inorder, vector<int>& postorder){
        if(postL > postR || inL > inR) return NULL;
        TreeNode* root = new TreeNode();
        root->val = postorder[postR];
        int k = inL;
        while(k<=inR && inorder[k]!=postorder[postR]) k++;
        int numL = k - inL;
        root->left = helper(postL,postL+numL-1, inL, k-1,inorder,postorder);
        root->right = helper(postL+numL, postR-1,k+1,inR,inorder,postorder);
        return root;
    }
};
```

