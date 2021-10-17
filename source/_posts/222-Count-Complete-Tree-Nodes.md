---
title: 222. Count Complete Tree Nodes
date: 2021-10-17 21:57:58
tags:
- LeetCode-medium
---

Given the `root` of a **complete** binary tree, return the number of the nodes in the tree.

According to **[Wikipedia](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)**, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between `1` and `2h` nodes inclusive at the last level `h`.

Design an algorithm that runs in less than `O(n)` time complexity.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/14/complete.jpg)

```
Input: root = [1,2,3,4,5,6]
Output: 6
```

 <!-- more -->

**Example 2:**

```
Input: root = []
Output: 0
```

**Example 3:**

```
Input: root = [1]
Output: 1
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5 * 104]`.
- `0 <= Node.val <= 5 * 104`
- The tree is guaranteed to be **complete**.

# Analysis

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/count-complete-tree-nodes/
 * Runtime: 32 ms, faster than 65.87%
 * Memory Usage: 30.9 MB, less than 63.42%
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
    int countNodes(TreeNode* root) {
        if(root == NULL) return 0;
        int right = 0;
        int left = 0;
        TreeNode* node = root;
        while(node){
            left++;
            node = node->left;
        }
        while(node){
            right++;
            node = node->right;
        }
        if(left == right) return (1<<left)-1;
        return countNodes(root->left)+countNodes(root->right)+1;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/count-complete-tree-nodes/
 * Runtime: 104 ms, faster than 81.11%
 * Memory Usage: 58.2 MB, less than 72.10% 
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
 * @return {number}
 */
var countNodes = function(root) {
    let left = 0, right = 0;
    let node = root;
    while(node){
        left++;
        node = node.left;
    }
    node = root;
    while(node){
        right++;
        node = node.right;
    }
    if(left == right) return (1<<left) - 1;
    return countNodes(root.left) + countNodes(root.right) + 1;
};
```

