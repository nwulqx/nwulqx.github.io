---
title: 103. Binary Tree Zigzag Level Order Traversal
date: 2021-10-13 22:37:08
tags:
- LeetCode-medium
- Queue(队列)
- BFS(广度优先遍历)
---

Given the `root` of a binary tree, return *the zigzag level order traversal of its nodes' values*. (i.e., from left to right, then right to left for the next level and alternate between).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
```

<!-- more -->

**Example 2:**

```
Input: root = [1]
Output: [[1]]
```

**Example 3:**

```
Input: root = []
Output: []
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-100 <= Node.val <= 100`

# 分析

**javascript**

```js
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/
 * Runtime: 76 ms, faster than 79.88% 
 * Memory Usage: 40.6 MB, less than 27.57%
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
 * @return {number[][]}
 */
var zigzagLevelOrder = function(root) {
    const res = [];
    if(!root) return res;
    const q = [];
    q.push(root);
    let zigzag = true;
    // 注意要写大于0
    while(q.length > 0){
        const len = q.length;
        const level = [];
        for(let i = 0; i < len; i++){
            const node = q.shift();
            if(zigzag) level.push(node.val);
            else level.unshift(node.val);
            if(node.left) q.push(node.left);
            if(node.right) q.push(node.right);
        }
        zigzag = !zigzag;
        res.push([...level]);
    }
    return res;
};
```

**c++**

```c++
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/
 * Runtime: 4 ms, faster than 60.49%
 * Memory Usage: 12.2 MB, less than 48.65% 
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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        bool zigzag = true;
        while(!q.empty()){
            int size = q.size();
            vector<int> level(size);
            for(int i = 0; i < size; i++){
                TreeNode* node = q.front();
                q.pop();
                int index = zigzag?i:size-i-1;
                level[index] = node->val;
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
            }
            zigzag = !zigzag;
            res.push_back(level);
        }
        return res;
    }
};
```

