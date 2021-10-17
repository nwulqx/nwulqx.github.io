---
title: 230. Kth Smallest Element in a BST
date: 2021-10-17 21:58:36
tags:
- LeetCode-medium
- recursion(递归)
- In-Order Traversal(中序遍历)
- Optimize(优化)
---

Given the `root` of a binary search tree, and an integer `k`, return *the* `kth` *smallest value (**1-indexed**) of all the values of the nodes in the tree*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg)

```
Input: root = [3,1,4,null,2], k = 1
Output: 1
```

 <!-- more -->

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg)

```
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
```

 

**Constraints:**

- The number of nodes in the tree is `n`.
- `1 <= k <= n <= 104`
- `0 <= Node.val <= 104`

 

**Follow up:** If the BST is modified often (i.e., we can do insert and delete operations) and you need to find the kth smallest frequently, how would you optimize?

# Analysis

**需要考虑优化问题，用非递归去解决**

## 非递归

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/kth-smallest-element-in-a-bst/
 * Runtime: 16 ms, faster than 85.13%
 * Memory Usage: 24.1 MB, less than 61.32%
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
    int kthSmallest(TreeNode* root, int k) {
        if(!root) return -1;
        stack<TreeNode*> st;
        int sum = 0;
        while(root || !st.empty()){
            if(root){
                st.push(root);
                root = root->left;
            }else{
                TreeNode* node = st.top();
                st.pop();
                sum++;
                if(sum == k) return node->val;
                root = node->right;
            }
        }
        return -1;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/kth-smallest-element-in-a-bst/
 * Runtime: 92 ms, faster than 56.82%
 * Memory Usage: 44.6 MB, less than 56.19%
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
 * @param {number} k
 * @return {number}
 */
var kthSmallest = function(root, k) {
    const st = [];
    let res = -1;
    if(!root) return res;
    let order = 0;
    while(root || st.length > 0){
        if(root){
            st.push(root);
            root = root.left;
        }else{
            let node = st.pop();
            order++;
            if(order==k){
                res = node.val;
                break;
            }
            root = node.right;
        }
    }
    return res;
};
```



## 递归思路

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/kth-smallest-element-in-a-bst/
 * Runtime: 16 ms, faster than 85.13%
 * Memory Usage: 24.2 MB, less than 33.35%
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
    int k, order = 0;
    int res = 0;
public:
    int kthSmallest(TreeNode* root, int k) {
        this->k = k;
        inorder(root);
        return res;
    }
    void inorder(TreeNode* node){
        if(node->left) inorder(node->left);
        order++;
        if(order == k){
            res = node->val;
            return;
        }  
        if(node->right) inorder(node->right);
        return;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/kth-smallest-element-in-a-bst/
 * Runtime: 84 ms, faster than 85.63%
 * Memory Usage: 44.9 MB, less than 43.89%
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
 * @param {number} k
 * @return {number}
 */
var kthSmallest = function(root, k) {
    let order = 0;
    let res = -1;
    function help(node){
        if(node.left) help(node.left);
        order++;
        if(order == k){
            res = node.val;
            return;
        }
        if(node.right) help(node.right);
    }
    help(root);
    return res;
};
```

