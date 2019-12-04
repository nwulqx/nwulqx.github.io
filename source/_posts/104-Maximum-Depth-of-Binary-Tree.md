---
title: 104. Maximum Depth of Binary Tree
date: 2017-05-08 16:55:15
tags:
- LeetCode-easy
- recursion(递归)
- Optimize(优化)
---
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

# BinaryTree Operation(二叉树操作)

> http://blog.csdn.net/luckyxiaoqiang/article/details/7518888

<!-- more -->
# Solution

## 思路：

1. 从下向上的思想，先得到左右子树的深度。
2. 选择左右子树中深度大的值+1作为当前深度返回上层。
3. 如果当前节点为空，应该返回0表示第0层（第0层是不存在的那一层，因为是空）

```java
public class MaximumDepthofBinaryTree3{
    public int maxDepth(TreeNode root) {
        return maxDepthHelp(root);
    }
    public int maxDepthHelp(TreeNode node) {
        if(node==null){
            return 0;
        }
        if(node.left==null && node.right==null){
            return 1;
        }
        return Math.max(maxDepthHelp(node.left),maxDepthHelp(node.right))+1;
    }
}
```

## Optimized(优化)

其实，仔细看，完全没有必要再去新建一个方法，因为参数和返回值完全一致。所以，只用在现有函数上既可。

```java
public class MaximumDepthofBinaryTree3{
    public int maxDepth(TreeNode root) {
        if(root==null){
            return 0;
        }
        return Math.max(maxDepth(root.left),maxDepth(root.right))+1;
    }
}
```

# 总结
>又是一道二叉树的问题，万变不离其宗，BFS，Stack，DFS，Queue，递归思路不能忘记！