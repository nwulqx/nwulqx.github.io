---
title: 173. Binary Search Tree Iterator
date: 2021-10-17 18:59:07
tags:
- LeetCode-medium
- recursion(递归)
- In-Order Traversal(中序遍历)
---

Implement the `BSTIterator` class that represents an iterator over the **[in-order traversal](https://en.wikipedia.org/wiki/Tree_traversal#In-order_(LNR))** of a binary search tree (BST):

- `BSTIterator(TreeNode root)` Initializes an object of the `BSTIterator` class. The `root` of the BST is given as part of the constructor. The pointer should be initialized to a non-existent number smaller than any element in the BST.
- `boolean hasNext()` Returns `true` if there exists a number in the traversal to the right of the pointer, otherwise returns `false`.
- `int next()` Moves the pointer to the right, then returns the number at the pointer.

Notice that by initializing the pointer to a non-existent smallest number, the first call to `next()` will return the smallest element in the BST.

You may assume that `next()` calls will always be valid. That is, there will be at least a next number in the in-order traversal when `next()` is called.

 <!-- more -->

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/25/bst-tree.png)

```
Input
["BSTIterator", "next", "next", "hasNext", "next", "hasNext", "next", "hasNext", "next", "hasNext"]
[[[7, 3, 15, null, null, 9, 20]], [], [], [], [], [], [], [], [], []]
Output
[null, 3, 7, true, 9, true, 15, true, 20, false]

Explanation
BSTIterator bSTIterator = new BSTIterator([7, 3, 15, null, null, 9, 20]);
bSTIterator.next();    // return 3
bSTIterator.next();    // return 7
bSTIterator.hasNext(); // return True
bSTIterator.next();    // return 9
bSTIterator.hasNext(); // return True
bSTIterator.next();    // return 15
bSTIterator.hasNext(); // return True
bSTIterator.next();    // return 20
bSTIterator.hasNext(); // return False
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 105]`.
- `0 <= Node.val <= 106`
- At most `105` calls will be made to `hasNext`, and `next`.

 

**Follow up:**

- Could you implement `next()` and `hasNext()` to run in average `O(1)` time and use `O(h)` memory, where `h` is the height of the tree?

# Analysis

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/binary-search-tree-iterator/
 * Runtime: 24 ms, faster than 89.53 %
 * Memory Usage: 24 MB, less than 97.90 %
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
class BSTIterator {
private:
    stack<TreeNode*> st;
public:
    BSTIterator(TreeNode* root) {
        addLeft(root);
    }
    
    int next() {
        TreeNode* node = st.top();
        st.pop();
        addLeft(node->right);
        return node->val;
    }
    
    bool hasNext() {
        return !st.empty();
    }
    void addLeft(TreeNode* node){
        while(node){
            st.push(node);
            node = node->left;
        }
    }
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator* obj = new BSTIterator(root);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```



**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/binary-search-tree-iterator/
 * Runtime: 140 ms, faster than 72.76% 
 * Memory Usage: 51.4 MB, less than 45.69%
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
 */
const st = [];
var addLeft = function(node) {
    while(node){
        st.push(node);
        node = node.left;
    }
};

var BSTIterator = function(root) {
    addLeft(root);
};

/**
 * @return {number}
 */
BSTIterator.prototype.next = function() {
    const node = st.pop();
    addLeft(node.right);
    return node.val;
};

/**
 * @return {boolean}
 */
BSTIterator.prototype.hasNext = function() {
    return st.length > 0;
};


/** 
 * Your BSTIterator object will be instantiated and called as such:
 * var obj = new BSTIterator(root)
 * var param_1 = obj.next()
 * var param_2 = obj.hasNext()
 */
```

