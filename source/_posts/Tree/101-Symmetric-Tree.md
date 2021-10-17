---
title: 101. Symmetric Tree
date: 2017-05-04 15:52:14
tags:
- LeetCode-easy
- Tree(树)
- recursion(递归)
- Stack(栈)
- Queue(队列)
- BFS(广度优先遍历)
- DFS(深度优先遍历)
---
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```c++
	    1
	   / \
	  2   2
	 / \ / \
	3  4 4  3
```

But the following `[1,2,2,null,3,null,3]` is not:

```c++
	    1
	   / \
	  2   2
	   \   \
	   3    3
```

<!-- more -->

同类题目：{% post_link 100-Same-Tree %}

# Solution

>这种树的问题一般两种思路：递归和非递归。<br>

## Solution1

**使用递归来解决，注意树的比较，是左子树的右节点和右子树的左节点比较，这样才是对称的。**

**javascript**

```js
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/symmetric-tree/submissions/
 * Runtime: 171 ms, faster than 5.15%
 * Memory Usage: 41 MB, less than 37.56%
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
 * @return {boolean}
 */
var isSymmetric = function(root) {
    function helper(left, right){
        if(!left && !right) return true;
        if((!left || !right) || (left.val != right.val)) return false;
        return helper(left.left, right.right) && helper(left.right, right.left);
    }
    if(!root) return ture;
    return helper(root.left, root.right);
};
```



**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/symmetric-tree/
 * Beats : 68.77%;
 */
struct TreeNode {
	int val;
	TreeNode *left;
	TreeNode *right;
	TreeNode() : val(0), left(nullptr), right(nullptr) {}
	TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
	TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

class Solution {
public:
	bool isSymmetric(TreeNode* root) {
		if (root == nullptr) return true;
		return isSymmetric(root->left, root->right);
	}
	bool isSymmetric(TreeNode* left, TreeNode* right) {
		if (left == nullptr && right == nullptr) return true;
		if (left == nullptr || right == nullptr) return false;
		if (left->val != right->val) return false;
		return isSymmetric(left->left, right->right) && isSymmetric(left->right, right->left);
	}
};
```



**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/symmetric-tree/
 * Beats : 40%;
 */
public class SymmetricTree{
    public boolean isSymmetric(TreeNode root) {
        if(root==null){
            return true;
        }
        if(root.left==null && root.right==null){
            return true;
        }
        if(root.left==null || root.right==null){
            return false;
        }
        return isSymmetricHelp(root.left,root.right);
    }
    public boolean isSymmetricHelp(TreeNode left,TreeNode right){
        if(left==null && right==null){
            return true;
        }
        if(left==null || right==null){
            return false;
        }
        if(left.val!=right.val){
            return false;
        }
        return help(left.left,right.right)&&help(left.right,right.left);
    }
}
```

## 非递归法

使用栈或者队列来解决，主要是借助栈或者队列来解决。

**BFS思路**

广度优先遍历主要借助队列这一数据结构。

```java
public class SymmetricTree{
    public boolean isSymmetric(TreeNode root){
        if(root==null){
            return true;
        }
        Queue<TreeNode> queue_p = new LinkedList<TreeNode>();
        Queue<TreeNode> queue_q = new LinkedList<TreeNode>();
        queue_p.add(root);
        queue_q.add(root);
        while(!queue_p.isEmpty()&&!queue_q.isEmpty()){
            TreeNode pn = queue_p.poll();
            TreeNode qn = queue_q.poll();
            if(pn.val!=qn.val){
                return false;
            }
            if(pn.left!=null){
                queue_p.add(pn.left);
            }
            if(qn.right!=null){
                queue_q.add(qn.right);
            }
            if(queue_p.size()!=queue_q.size()){
                return false;
            }
            if(pn.right!=null){
                queue_p.add(pn.right);
            }
            if(qn.left!=null){
                queue_q.add(qn.left);
            }
            if(queue_p.size()!=queue_q.size()){
                return false;
            }
        }
        return queue_p.size()==queue_q.size();
    }
}
```

**DFS思路**

深度优先遍历主要借助栈这一数据结构。

```java
public class SymmetricTree2{
    public boolean isSymmetric(TreeNode root){
        if(root==null){
            return true;
        }
        if(root.left==null && root.right==null){
            return true;
        }
        if(root.left==null || root.right==null){
            return false;
        }
        Stack<TreeNode> stack_left = new Stack<TreeNode>();
        Stack<TreeNode> stack_right = new Stack<TreeNode>();
        if(root.left!=null){
            stack_left.push(root.left);
        }
        if(root.right!=null){
            stack_right.push(root.right);
        }
        if(stack_right.size()!=stack_left.size()){
            return false;
        }
        if(root.left.val!=root.right.val){
            return false;
        }
        while(!stack_left.empty()&&!stack_right.empty()){
            TreeNode left = stack_left.pop();
            TreeNode right = stack_right.pop();
            if(left.val!=right.val){
                return false;
            }
            if(left.left!=null){
                stack_left.push(left.left);
            }
            if(right.right!=null){
                stack_right.push(right.right);
            }
            if(stack_left.size()!=stack_right.size()){
                return false;
            }
            if(left.right!=null){
                stack_left.push(left.right);
            }
            if(right.left!=null){
                stack_right.push(right.left);
            }
            if(stack_left.size()!=stack_right.size()){
                return false;
            }
        }
        return stack_right.size()==stack_left.size();
    }
}
```

# 总结

注意深度优先遍历和广度优先遍历，这里两处的代码基本可以说是一致的，但是由于使用的栈和队列的数据结构完全不相同，所以两种思路是完全不同的。不得不感慨数据结构的强大，虽然代码逻辑完全一样，但是由于使用了不同的数据结构，却出现了两种不同的解决思路。

