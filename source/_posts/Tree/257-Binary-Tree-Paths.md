---
title: 257. Binary Tree Paths
date: 2021-10-17 23:18:40
tags:
- LeetCode-easy
- recursion(递归)
---

Given the `root` of a binary tree, return *all root-to-leaf paths in **any order***.

A **leaf** is a node with no children.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/12/paths-tree.jpg)

```
Input: root = [1,2,3,null,5]
Output: ["1->2->5","1->3"]
```

 <!-- more -->

**Example 2:**

```
Input: root = [1]
Output: ["1"]
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 100]`.
- `-100 <= Node.val <= 100`

# Analysis

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/binary-tree-paths/
 * Runtime: 4 ms, faster than 75.06 %
 * Memory Usage: 13.1 MB, less than 48.21 %
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
    vector<string> res;
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        dfs(root, ""+to_string(root->val));
        return res;
    }
    void dfs(TreeNode* node, string path){
        if(!node->left && !node->right) res.push_back(path);
        if(node->left) dfs(node->left,path+"->"+to_string(node->left->val));
        if(node->right) dfs(node->right,path+"->"+to_string(node->right->val));
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/binary-tree-paths/
 * Runtime: Runtime: 80 ms, faster than 69.58%
 * Memory Usage: 40.4 MB, less than 17.83%
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
 * @return {string[]}
 */
var binaryTreePaths = function(root) {
    const res = [];
    function dfs(node, path){
        if(!node.left && !node.right){
            res.push(path);
            return;
        }
        if(node.left) dfs(node.left, path+'->'+node.left.val);
        if(node.right) dfs(node.right, path+'->'+node.right.val);
    }
    dfs(root, ''+root.val);
    return res;
};
```

