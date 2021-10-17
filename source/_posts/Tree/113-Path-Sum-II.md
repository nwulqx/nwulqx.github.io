---
title: 113. Path Sum II
date: 2021-10-17 16:34:43
tags:
- LeetCode-medium
- recursion(递归)
---

Given the `root` of a binary tree and an integer `targetSum`, return *all **root-to-leaf** paths where the sum of the node values in the path equals* `targetSum`*. Each path should be returned as a list of the node **values**, not node references*.

A **root-to-leaf** path is a path starting from the root and ending at any leaf node. A **leaf** is a node with no children.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg)

```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]
Explanation: There are two paths whose sum equals targetSum:
5 + 4 + 11 + 2 = 22
5 + 8 + 4 + 5 = 22
```

<!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```
Input: root = [1,2,3], targetSum = 5
Output: []
```

**Example 3:**

```
Input: root = [1,2], targetSum = 0
Output: []
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5000]`.
- `-1000 <= Node.val <= 1000`
- `-1000 <= targetSum <= 1000`

# 分析

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/path-sum-ii/
 * Runtime: 84 ms, faster than 89.05% 
 * Memory Usage: 41.8 MB, less than 74.27%
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
 * @param {number} targetSum
 * @return {number[][]}
 */
var pathSum = function(root, targetSum) {
    const res = [];
    const path = [];
    function dfs(node, target){
        if(!node) return;
        path.push(node.val);
        if(!node.left && !node.right && target === node.val){
            res.push([...path]);
            path.pop();
            return;
        }
        dfs(node.left, target-node.val);
        dfs(node.right, target-node.val);
        path.pop();
    }
    dfs(root, targetSum);
    return res;
};
```



**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/path-sum-ii/
 * Runtime: 8 ms, faster than 83.61% 
 * Memory Usage: 19.7 MB, less than 93.14% 
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
    vector<vector<int>> res;
    vector<int> path;
public:
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        dfs(root, targetSum);
        return res;
    }
    void dfs(TreeNode* node, int target){
        if(node == NULL) return;
        path.push_back(node->val);
        if(node->left==NULL && node->right==NULL && node->val == target){
            res.push_back(path);
        }
        dfs(node->left,target-node->val);
        dfs(node->right,target-node->val);
        path.pop_back();
    }
};
```

