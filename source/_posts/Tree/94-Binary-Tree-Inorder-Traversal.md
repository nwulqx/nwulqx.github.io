---
title: 94. Binary Tree Inorder Traversal
date: 2017-05-19 18:16:30
tags:
- LeetCode-easy
- recursion(递归)
- In-Order Traversal(中序遍历)
- Morris Traversal
- Tree
---

Given the `root` of a binary tree, return *the inorder traversal of its nodes' values*.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
Input: root = [1,null,2,3]
Output: [1,3,2]
```

<!-- more -->

**Example 2:**

```
Input: root = []
Output: []
```

**Example 3:**

```
Input: root = [1]
Output: [1]
```

**Example 4:**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_5.jpg)

```
Input: root = [1,2]
Output: [2,1]
```

**Example 5:**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_4.jpg)

```
Input: root = [1,null,2]
Output: [1,2]
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

 

**Follow up:** Recursive solution is trivial, could you do it iteratively?

# Solution

## Solution1

**使用递归(Recursion)**

**java**
```java
public class BinaryTreeInorderTraversal{
    // Using recursiuon!
    public List<Integer> inorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        if(root==null){
            return list;
        }
        helper(list,root);
        return list;
    }
    public void helper(ArrayList<Integer> list, TreeNode node){
        if(node.left!=null){
            helper(list,node.left);
        }
        list.add(node.val);
        if(node.right!=null){
            helper(list,node.right);
        }
    }
}
```

>不说了，递归还是很容易理解的。

## Solution2

**不使用递归(Without using recursion)**

>中序遍历非递归借助栈的实现方法。

**c++**

```c++
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/binary-tree-inorder-traversal/
 * 4 ms, faster than 43.54 % 
 * Memory Usage: 8.4 MB, less than 63.67 %
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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        if(!root) return res;
        stack<TreeNode*> st;
        TreeNode* node = root;
        while(node || !st.empty()){
            while(node){
                st.push(node);
                node = node->left;
            }
            node = st.top();
            st.pop();
            res.push_back(node->val);
            node = node->right;
        }
        return res;
    }
};
```



**javascript**

```javascript
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/binary-tree-inorder-traversal/
 * Runtime: 95 ms, faster than 27.10%
 * Memory Usage: 38.8 MB, less than 65.00%
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
 * @return {number[]}
 */
var inorderTraversal = function(root) {
    const res = [];
    if(!root) return res;
    const st = [];
    while(root || st.length){
        while(root){
            st.push(root);
            root = root.left;
        }
        root = st.pop();
        res.push(root.val);
        root = root.right;
    }
    return res;
};
```

**java**

```java
public class BinaryTreeInorderTraversal2{
    // Without using recursion!
    public List<Integer> inorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode node = root;
        while(node!=null || !stack.empty()){
            if(node!=null){
                stack.push(node);
                node = node.left;
            }else{
                TreeNode p = stack.pop();
                list.add(p.val);
                node = p.right;
            }
        }
        return list;
    }
}
```

## Solution3

**最优解**

**Morris traversal**

>时间复杂度：O(n)
>空间复杂度：O(1)

**java**
```java
public class BinaryTreeInorderTraversal{
    // Morris Traversal !
    public List<Integer> inorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        TreeNode cur = root;
        while(cur!=null){
            if(cur.left==null){
                list.add(cur.val);
                cur = cur.right;
            }else{
                TreeNode pre = cur.left;
                while(pre.right!=null && pre.right!=cur){
                    pre = pre.right;
                }
                if(pre.right==null){
                    pre.right = cur;
                    cur = cur.left;
                }else{
                    list.add(cur.val);
                    pre.right = null;
                    cur = cur.right;
                }
            }
        }
        return list;
    }
}
```

# 总结

>递归和非递归的思路应该注意。同时也应该熟练Morris Traversal。