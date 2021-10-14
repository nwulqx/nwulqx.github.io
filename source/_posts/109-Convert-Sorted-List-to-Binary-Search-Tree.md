---
title: 109. Convert Sorted List to Binary Search Tree
date: 2021-10-14 22:50:23
tags:
- LeetCode-medium
- Tree(树)
- recursion(递归)
- Queue(队列)
- BFS(广度优先遍历)
- DFS(深度优先遍历)
---

Given the `root` of a binary tree, return *the bottom-up level order traversal of its nodes' values*. (i.e., from left to right, level by level from leaf to root).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[15,7],[9,20],[3]]
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
- `-1000 <= Node.val <= 1000`

# 分析

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/
 * Runtime: 140 ms, faster than 19.31% 
 * Memory Usage: 44.4 MB, less than 20.46%
 */
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
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
 * @param {ListNode} head
 * @return {TreeNode}
 */
var sortedListToBST = function(head) {
    function help(start, end){
        if(start > end) return null;
        const mid = Math.trunc(start + (end-start)/2);
        const left = help(start, mid - 1);
        const root = new TreeNode();
        root.val = head.val;
        head = head.next;
        root.left = left;
        root.right = help(mid+1, end);
        return root;
    }
    let node = head;
    if(!head) return null;
    let n = 0;
    while(node){
        n++;
        node = node.next;
    }
    return help(0, n-1);
};
```



**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/
 * Runtime: 43 ms, faster than 32.40%
 * Memory Usage: 31.1 MB, less than 35.05%
 */
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
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
    ListNode* head = NULL;
public:
    TreeNode* sortedListToBST(ListNode* head) {
        if(!head) return NULL;
        ListNode* node = head;
        this->head = head;
        int n = 0;
        while(node){
            n++;
            node = node->next;
        }
        return help(0,n-1);
    }
    TreeNode* help(int start, int end){
        if(start>end || !head) return NULL;
        int mid = start + (end - start)/2;
        TreeNode* left = help(start, mid - 1);
        TreeNode* root = new TreeNode();
        root->val = head->val;
        head = head->next;
        root->left = left;
        
        root->right = help(mid+1, end);
        return root;
    }
};
```

