---
title: 117. Populating Next Right Pointers in Each Node II
date: 2021-10-17 17:53:29
tags:
- LeetCode-medium
---

Given a binary tree

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

![img](https://assets.leetcode.com/uploads/2019/02/15/117_sample.png)

```
Input: root = [1,2,3,4,5,null,7]
Output: [1,#,2,3,#,4,5,7,#]
Explanation: Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

<!-- more -->

**Example 2:**

```
Input: root = []
Output: []
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 6000]`.
- `-100 <= Node.val <= 100`

 

**Follow-up:**

- You may only use constant extra space.
- The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

# Analysis

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/
 * Runtime: 8 ms, faster than 96.78%
 * Memory Usage: 17.4 MB, less than 80.14%
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
        while(node){
            Node* pre = new Node();
            Node* temp = pre;
            while(node){
                if(node->left){
                    pre->next = node->left;
                    pre = pre->next;
                }
                if(node->right){
                    pre->next = node->right;
                    pre = pre->next;
                }
                node = node->next;
            }
            node = temp->next;
        }
        return root;
    }
};
```



**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/
 * Runtime: 92 ms, faster than 87.88%
 * Memory Usage: 43.9 MB, less than 32.39%
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
        let pre = new Node();
        let temp = pre;
        while(node){
            if(node.left){
                pre.next = node.left;
                pre = pre.next;
            }
            if(node.right){
                pre.next = node.right;
                pre = pre.next;
            }
            node = node.next;
        }
        node = temp.next;
    }
    return root;
};
```

