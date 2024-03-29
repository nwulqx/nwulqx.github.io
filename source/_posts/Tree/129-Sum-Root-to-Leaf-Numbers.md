---
title: 129. Sum Root to Leaf Numbers
date: 2021-10-17 17:53:58
tags:
- LeetCode-medium
---

You are given the `root` of a binary tree containing digits from `0` to `9` only.

Each root-to-leaf path in the tree represents a number.

- For example, the root-to-leaf path `1 -> 2 -> 3` represents the number `123`.

Return *the total sum of all root-to-leaf numbers*. Test cases are generated so that the answer will fit in a **32-bit** integer.

A **leaf** node is a node with no children.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/num1tree.jpg)

```
Input: root = [1,2,3]
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```

<!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/02/19/num2tree.jpg)

```
Input: root = [4,9,0,5,1]
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 1000]`.
- `0 <= Node.val <= 9`
- The depth of the tree will not exceed `10`.

# Analysis

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/sum-root-to-leaf-numbers/
 * Runtime: 4 ms, faster than 49.64 %
 * Memory Usage: 9.3 MB, less than 43.71 %
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
    int res = 0;
public:
    int sumNumbers(TreeNode* root) {
        dfs(root, 0);
        return res;
    }
    void dfs(TreeNode* node, int sum){
        if(node == NULL) return;
        sum = (sum*10 + node->val);
        if(!node->left && !node->right){
            res += sum;
            return;
        }
        dfs(node->left,sum);
        dfs(node->right,sum);
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/sum-root-to-leaf-numbers/
 * Runtime: 68 ms, faster than 95.64%
 * Memory Usage: 40.3 MB, less than 10.71%
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
var sumNumbers = function(root) {
    let res = 0;
    function dfs(node, sum){
        if(!node) return;
        sum = (sum*10 + node.val);
        if(!node.left && !node.right){
            res += sum;
            return;
        }
        dfs(node.left, sum);
        dfs(node.right, sum);
    }
    dfs(root, 0);
    return res;
};
```

