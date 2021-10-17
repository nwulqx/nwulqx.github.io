---
title: 104. Maximum Depth of Binary Tree
date: 2017-05-08 16:55:15
tags:
- LeetCode-easy
- Tree(树)
- recursion(递归)
---
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree `[3,9,20,null,null,15,7]`,

```c++
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.

<!-- more -->

# Solution

## 思路：

采用递归的思路解决。

**javascript**

```js
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/maximum-depth-of-binary-tree/
 * Runtime: 124 ms, faster than 15.63%
 * Memory Usage: 41.3 MB, less than 96.06%
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
var maxDepth = function(root) {
    if(!root) return 0;
    return Math.max(maxDepth(root.left),maxDepth(root.right)) + 1;
};
```



**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/maximum-depth-of-binary-tree/
 * Beats : 83.16%;
 */
class Solution {
public:
	int maxDepth(TreeNode* root) {
		if (root == nullptr) return 0;
		int left = maxDepth(root->left);
		int right = maxDepth(root->right);
		return left > right ? left + 1 : right + 1;
	}
};
```



**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/maximum-depth-of-binary-tree/
 * Beats : 40%;
 */
public class MaximumDepthofBinaryTree{
    public int maxDepth(TreeNode root) {
        if(root==null){
            return 0;
        }
        return Math.max(maxDepth(root.left),maxDepth(root.right))+1;
    }
}
```

# 总结
一道二叉树的问题，万变不离其宗，BFS，Stack，DFS，Queue，递归思路不能忘记！