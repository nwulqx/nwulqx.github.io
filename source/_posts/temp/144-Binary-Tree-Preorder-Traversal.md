---
title: 144. Binary Tree Preorder Traversal
date: 2017-05-19 17:20:52
tags:
- LeetCode-medium
- recursion(递归)
- Pre-Order Traversal(先序遍历)
- Morris Traversal
---

Given a binary tree, return the preorder traversal of its nodes' values.

For example:
Given binary tree `{1,#,2,3}`,


	   1
	    \
	     2
	    /
	   3

return [1,2,3].

Note: Recursive solution is trivial, could you do it iteratively?

<!-- more -->

# Solution

## Solution1

**使用递归(Recursion)**

```java
public class BinaryTreePreorderTraversal{
    // Using recursion!
    public List<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        preorderHelper(list,root);
        return list;
    }
    public void preorderHelper(ArrayList<Integer> list, TreeNode node){
        if(node==null){
            return;
        }
        list.add(node.val);
        preorderHelper(list,node.left);
        preorderHelper(list,node.right);
    }
}
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}
```

>总的来说，递归的思路还是易于操作理解。

## Solution2

**不使用递归(Without using recursion)**

>主要借助栈，存取每一次的根节点，然后每次弹出栈顶元素，然后遍历右子树。

```java
public class BinaryTreePreorderTraversal3{
    // Without using recursion!
    public List<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode node = root;
        while(node!=null || !stack.empty()){
            if(node!=null){
                list.add(node.val);
                stack.push(node);
                node = node.left;
            }else{
                TreeNode p = stack.pop();
                node = p.right;
            }
        }
        return list;
    }
}
```

## Solution3

**不使用递归(Without using recursion)**

>仍然是不使用递归的思路，与Solution2不同的是，对于栈的使用有所不同。此方法中，更像是BFS的思路，按层来遍历，将每层的右节点存入栈中。然后利用栈的性质：“后进先出”，待到左节点为空时，再依次取出栈中元素。

```java
public class BinaryTreePreorderTraversal{
    public List<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode node = root;
        while(node!=null){
            list.add(node.val);
            if(node.right!=null){
                stack.push(node.right);
            }
            node = node.left;
            if(node==null && !stack.empty()){
                node = stack.pop();
            }
        }
        return list;
    }
}
```
## Solution4

>上述3种方法是最常用的遍历二叉树的方法，其时间、空间复杂度均为O(n)。
>下面说一种名为Morris Traversal（莫里斯遍历），其时间复杂度为O(n)，但是由于没有借助栈，所以其空间复杂度为O(1)。

**Morris traversal**

```java
public class BinaryTreePreorderTraversal3{
    // Morris Traversal !
    public List<Integer> preorderTraversal(TreeNode root) {
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
                    list.add(cur.val);
                    pre.right = cur;
                    cur = cur.left;
                }else{
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

>介绍了四种遍历方法，分为三种类型：
>1. 递归法，这种方式便于理解，代码简洁。
>2. 非递归法，两种思路，一种是利用栈存储根节点，然后每次弹出后访问其右孩子节点；另一种是按层，每次存储向左遍历的根节点的右孩子节点，然后当左节点为叶节点时，按照栈的顺序弹出栈中元素。
>3. 莫里斯遍历，利用对于是否访问过该节点判断是否是回溯还是第一次向下遍历。
对于先序，中序，后序的遍历，是用递归都是最易于理解的。使用循环操作是相对麻烦的。同时，对于栈的灵活应用也是应该值得学习的。