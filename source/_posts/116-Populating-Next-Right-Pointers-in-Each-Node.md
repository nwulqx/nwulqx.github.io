---
title: 116. Populating Next Right Pointers in Each Node
date: 2021-10-17 16:35:29
tags:
- LeetCode-medium
---

You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

```
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

<!-- more -->

**Example 2:**

```
Input: root = []
Output: []
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 212 - 1]`.
- `-1000 <= Node.val <= 1000`

 

**Follow-up:**

- You may only use constant extra space.
- The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

# 分析

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/populating-next-right-pointers-in-each-node/
 * Runtime: 104 ms, faster than 53.17%
 * Memory Usage: 44.8 MB, less than 97.95%
 */
/**
 * // Definition for a Node.
 * function Node(val, left, right, next) {
 *    this.val = val === undefined ? null : val;
 *    this.left = left === undefined ? null : left;
 *    this.right = right === undefined ? null : right;
 *    this.next = next === undefined ? null : next;
 * };
 */

/**
 * @param {Node} root
 * @return {Node}
 */
var connect = function(root) {
    let node = root;
    while(node){
        let temp = node;
        while(node){
            if(node.left) node.left.next = node.right;
            if(node.right && node.next) node.right.next = node.next.left;
            node = node.next;
        }
        node = temp.left;
    }
    return root;
};
```



**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/populating-next-right-pointers-in-each-node/
 * Runtime: 16 ms, faster than 90.92% 
 * Memory Usage: 16.8 MB, less than 66.61%
 */
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        Node* node = root;
        while(node != NULL){
            Node* temp = node;
            while(node != NULL){
                if(node->left != NULL) node->left->next = node->right;
                if(node->next != NULL && node->right != NULL) node->right->next = node->next->left;
                node = node->next;
            }
            node = temp->left;
        }
        return root;
    }
};
```

