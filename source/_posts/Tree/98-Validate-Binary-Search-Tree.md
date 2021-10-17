---
title: 98. Validate Binary Search Tree
date: 2021-10-13 21:49:36
tags:
- LeetCode-medium
- In-Order Traversal(中序遍历)
- Tree
---

Given the `root` of a binary tree, *determine if it is a valid binary search tree (BST)*.

A **valid BST** is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

```
Input: root = [2,1,3]
Output: true
```

  <!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

```
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-231 <= Node.val <= 231 - 1`

# 分析

## 递归

**c++**

```c++
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/validate-binary-search-tree/
 * Runtime: 19 ms, faster than 22.50 %
 * Memory Usage:  21.6 MB, less than  89.34 %
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
    TreeNode* pre;
public:
    bool isValidBST(TreeNode* root) {
        if(!root) return true;
        bool left = isValidBST(root->left);
        if(!left) return false;
        if(pre && pre->val >= root->val){
            return false;
        }
        pre = root;
        return isValidBST(root->right);
    }
};
```



**javascript**

```javascript
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/validate-binary-search-tree/
 * Runtime: 136 ms, faster than 16.76% 
 * Memory Usage: 42.5 MB, less than 98.77%
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
 * @return {boolean}
 */
var isValidBST = function(root) {
    let pre = null;
    var preorder = function(node){
        if(!node) return true;
        if(!preorder(node.left)) return false;
        if(pre && pre.val >= node.val) return false;
        pre = node;
        return preorder(node.right);
    }
    if(!root) return true;
    return preorder(root);
};
```



## 非递归

**c++**

```c++
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/validate-binary-search-tree/
 * Runtime: 34 ms, faster than 5.53%
 * Memory Usage: 21.9 MB, less than 15.36% 
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
    bool isValidBST(TreeNode* root) {
        if(!root) return true;
        stack<TreeNode*> st;
        TreeNode* pre = NULL;
        while(root || !st.empty()){
            while(root){
                st.push(root);
                root = root->left;
            }
            root = st.top();
            st.pop();
            if(pre && pre->val >= root->val){
                return false;
            }
            pre = root;
            root = root->right;
        }
        return true;
    }
};
```



**javascript**

```javascript
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/validate-binary-search-tree/
 * Runtime: 139 ms, faster than 15.17% 
 * Memory Usage: 43.2 MB, less than 63.66% 
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
 * @return {boolean}
 */
var isValidBST = function(root) {
    if(!root) return true;
    const st = [];
    let pre = null;
    while(root || st.length > 0){
        while(root){
            st.push(root);
            root = root.left;
        }
        root = st.pop();
        if(pre && pre.val >= root.val) return false;
        pre = root;
        root = root.right;
    }
    return true;
};
```

