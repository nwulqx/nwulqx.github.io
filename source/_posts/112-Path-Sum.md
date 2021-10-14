---
title: 112. Path Sum
date: 2017-05-19 17:06:31
tags:
- LeetCode-easy
- recursion(递归)
- Stack(栈)
- Post-Order Traversal(后序遍历)
---

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

**For example:**<br>
Given the below binary tree and `sum = 22`,

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1

return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.

<!-- more -->

# Solution
## Solution1

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/path-sum/
 * Runtime: 136 ms, faster than 15.48%
 * Memory Usage: 42.5 MB, less than 73.20%
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
 * @return {boolean}
 */
var hasPathSum = function(root, targetSum) {
    if(!root) return false;
    if(!root.left && !root.right){
        return targetSum === root.val;
    }
    return hasPathSum(root.left, targetSum-root.val) || hasPathSum(root.right, targetSum-root.val);
};
```



**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/path-sum/
 * Runtime: 350 ms, faster than 25.19% 
 * Memory Usage: 102.2 MB, less than 29.91%
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
    bool hasPathSum(TreeNode* root, int targetSum) {
        if(!root) return false;
        if(!root->left && !root->right){
            return targetSum == root->val;
        }
        return hasPathSum(root->left, targetSum-root->val) || hasPathSum(root->right, targetSum-root->val);
    }
};
```

**java**

```java
public class PathSum{
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root==null){
            return false;
        }
        if(root.left==null&&root.right==null){
            return sum==root.val;
        }
        return hasPathSum(root.right,sum-root.val)||hasPathSum(root.left,sum-root.val);
    }
}
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}
```

## Solution2

**postorder traversal(后序遍历)**

>利用后序遍历找出符合条件的答案。

```java
public class PathSum{
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root==null){
            return false;
        }
        Stack<TreeNode> stack = new Stack<TreeNode>();
        int SUM = 0;
        TreeNode node = root,pre=null;
        while(node!=null || !stack.empty()){
            while(node!=null){
                stack.push(node);
                SUM += node.val;
                node = node.left;
            }
            node = stack.peek();
            if(node.left==null&&node.right==null&&sum==SUM){
                return true;
            }
            if(node.right!=null && pre!=node.right){
                node = node.right;
            }else{
                SUM -= node.val;
                pre = node;
                stack.pop();
                node = null;
            }
        }
        return false;
    }
}
```

**另一种后序遍历的常用写法**

```java
public class PathSum3{
    public boolean hasPathSum(TreeNode root, int sum) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        int SUM = 0;
        TreeNode node = root,pre = null;
        while(node!=null || !stack.empty()){
            if(node!=null){
                stack.push(node);
                SUM += node.val;
                node = node.left;
            }else{
                TreeNode p = stack.peek();
                if(p.left==null&&p.right==null&&SUM==sum){
                    return true;
                }
                if(p.right!=null&&pre!=p.right){
                    node = p.right;
                }else{
                    SUM -= p.val;
                    pre = p;
                    stack.pop();
                    node = null;
                }
            }
        }
        return false;
    }
}
```

# 总结

>后序遍历的循环操作二叉树是需要理解下的。在本题中，需要再更进一步，利用栈来组合新的和。