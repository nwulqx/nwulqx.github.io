---
title: 94. Binary Tree Inorder Traversal
date: 2017-05-19 18:16:30
tags:
- LeetCode-medium
- recursion(递归)
- In-Order Traversal(中序遍历)
- Morris Traversal
---

Given a binary tree, return the inorder traversal of its nodes' values.

For example:
Given binary tree [1,null,2,3],

	   1
	    \
	     2
	    /
	   3

return [1,3,2].

Note: Recursive solution is trivial, could you do it iteratively?

<!-- more -->
# Solution

## Solution1

**使用递归(Recursion)**

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

**Morris traversal**

>时间复杂度：O(n)
>空间复杂度：O(1)

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