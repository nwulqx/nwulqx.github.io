---
title: 111. Minimum Depth of Binary Tree
date: 2017-05-11 14:42:37
tags:
- LeetCode-easy
- recursion(递归)
- Optimize(优化)
- Boundary Check(边界值检测)
- BFS(广度优先遍历)
- DFS(深度优先遍历)
---
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

<!-- more -->
# Solution

## Solution1

### 递归解决

**Boundary Check(边界值检测)**

>从尾部向上递归：
>1. 当前节点为空，返回0；
>2. 当前节点的左右节点均为空，返回1；
>3. 当前节点的左右节点中有一个为空，则应该返回不为空的节点的子树最小深度。
>4. 当前节点的左右节点均不为空，则应该返回深度小的节点。

```java
public class MinimumDepthofBinaryTree{
    // Using DFS
    public int minDepth(TreeNode root) {
        if(root==null){
            return 0;
        }
        if(root.left==null&&root.right==null){
            return 1;
        }
        if(root.left==null||root.right==null){
            return Math.max(minDepth(root.left),minDepth(root.right))+1;
        }
        return Math.min(minDepth(root.left),minDepth(root.right))+1;
    }
}
```
**Attention**

		if(root.left==null||root.right==null){
			return Math.max(minDepth(root.left),minDepth(root.right))+1;
		}

>注意返回值，如果一个节点只存在一个左或者右节点，那么不这么写的话，会返回空节点的深度。

	       1
	      /
	     2
	    /
	   3

>对于这样的树，可能会返回深度1，因为右子树深度为0。

## Solution2

### 非递归解决

**BFS方案**

>按照广度优先`按层`遍历节点：
>1. 某一结点的左右子树均为空，则应该返回当前深度。
>2. 其他情况则继续按照BFS遍历节点。

```java
public class MinimumDepthofBinaryTree{
    // Using BFS
    public int minDepth(TreeNode root) {
        if(root==null){
            return 0;
        }
        if(root.left==null&&root.right==null){
            return 1;
        }
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.add(root);
        int level = 1;
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i=0;i<size;i++){
                TreeNode node = queue.poll();
                if(node.left==null&&node.right==null){
                    return level;
                }
                if(node.left!=null){
                    queue.add(node.left);
                }
                if(node.right!=null){
                    queue.add(node.right);
                }
            }
            level++;
        }
        return level;
    }
}
```

# 总结

>1. 注意leaf node的定义，即没有左右子树；
>2. 注意此题中，对于一些边界检测的判断，只含有一个子树时，应该以存在的子树继续计算深度。