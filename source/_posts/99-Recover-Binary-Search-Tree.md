---
title: 99. Recover Binary Search Tree
date: 2021-10-13 22:02:06
tags:
- LeetCode-medium
- In-Order Traversal(中序遍历)
- Tree
---

You are given the `root` of a binary search tree (BST), where the values of **exactly** two nodes of the tree were swapped by mistake. *Recover the tree without changing its structure*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/28/recover1.jpg)

```
Input: root = [1,3,null,null,2]
Output: [3,1,null,null,2]
Explanation: 3 cannot be a left child of 1 because 3 > 1. Swapping 1 and 3 makes the BST valid.
```

  <!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/10/28/recover2.jpg)

```
Input: root = [3,1,4,null,null,2]
Output: [2,1,4,null,null,3]
Explanation: 2 cannot be in the right subtree of 3 because 2 < 3. Swapping 2 and 3 makes the BST valid.
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[2, 1000]`.
- `-231 <= Node.val <= 231 - 1`

 

**Follow up:** A solution using `O(n)` space is pretty straight-forward. Could you devise a constant `O(1)` space solution?

# 分析

## 注意点

**first和second的赋值是很重要的考虑，具体赋什么值可以自行画个例子~**

![](.\99. Recover Binary Search Tree.png)

**javascript**

```js
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/recover-binary-search-tree/submissions/
 * Runtime: 296 ms, faster than 11.48% 
 * Memory Usage: 48.6 MB, less than 34.43%
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
var recoverTree = function(root) {
    let pre = null, first = null, second = null;
    var inorder = function(node){
        if(!node) return;
        inorder(node.left);
        if(!first && pre && pre.val >= node.val){
            first = pre;
        }
        if(first && pre && pre.val >= node.val){
            second = node;
        }
        pre = node;
        inorder(node.right);
    }
    inorder(root);
    const tmp = first.val;
    first.val = second.val;
    second.val = tmp;
};
```



**c++**

```c++
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/recover-binary-search-tree/submissions/
 * Runtime: Runtime: 20 ms, faster than 95.52%
 * Memory Usage: Memory Usage: 57.8 MB, less than 87.66%
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
    TreeNode* first = NULL, *second = NULL, *pre = NULL;
public:
    void recoverTree(TreeNode* root) {
        dfs(root);
        int temp = first->val;
        first->val = second->val;
        second->val = temp;
    }
    void dfs(TreeNode* node){
        if(!node) return;
        dfs(node->left);
        if(!first && pre && pre->val >= node->val){
            first = pre;
        }
        if(first && pre && pre->val >= node->val){
            second = node;
        }
        pre = node;
        dfs(node->right);
    }
};
```

