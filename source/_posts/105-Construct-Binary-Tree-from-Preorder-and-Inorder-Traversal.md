---
title: 105. Construct Binary Tree from Preorder and Inorder Traversal
date: 2021-10-13 23:20:16
tags:
- LeetCode-easy
- Tree(树)
- recursion(递归)
- In-Order Traversal(中序遍历)
---

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return *the binary tree*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

<!-- more -->

**Example 2:**

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

 # 分析

**javascript**

```js
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/
 * Runtime: 141 ms, faster than 44.67% 
 * Memory Usage: 41.5 MB, less than 95.68%
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
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */
var buildTree = function(preorder, inorder) {
    function helper(preL, preR, inL, inR){
        if(preL > preR || inL > inR) return null;
        const root = new TreeNode();
        root.val = preorder[preL];
        let k = inL;
        while(k!==inR && inorder[k]!==preorder[preL]){
            k++;
        }
        const numL = k-inL;
        root.left = helper(preL+1, preL+numL,inL,k-1);
        root.right = helper(preL+numL+1,preR,k+1,inR);
        return root;
    }
    const n = preorder.length;
    const m = inorder.length;
    return helper(0,n-1,0,m-1);
};
```

**c++**

```c++
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/
 * Runtime: 40 ms, faster than 30.38 %
 * Memory Usage: 26.1 MB, less than 60.79 %
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
    vector<int> preorder;
    vector<int> inorder;
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        this->preorder = preorder;
        this->inorder = inorder;
        int n = preorder.size();
        int m = inorder.size();
        return helper(0,n-1,0,m-1);
    }
    TreeNode* helper(int preL, int preR, int inL, int inR){
        if(preL > preR || inL > inR) return NULL;
        TreeNode* root = new TreeNode();
        root->val = preorder[preL];
        int k = inL;
        while(k<=inR && inorder[k]!=preorder[preL]) k++;
        int numL = k - inL;
        root->left = helper(preL+1,preL+numL, inL, k-1);
        root->right = helper(preL+numL+1, preR,k+1,inR);
        return root;
    }
};
```

