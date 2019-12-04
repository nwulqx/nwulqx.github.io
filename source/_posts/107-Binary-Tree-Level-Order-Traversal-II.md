---
title: 107. Binary Tree Level Order Traversal II
date: 2017-05-08 17:54:47
tags:
- LeetCode-easy
- recursion(递归)
- Queue(队列)
- BFS(广度优先遍历)
- DFS(深度优先遍历)
---
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

	    3
	   / \
	  9  20
	    /  \
	   15   7
return its bottom-up level order traversal as:

		[
		  [15,7],
		  [9,20],
		  [3]
		]

<!-- more -->
# Solution

## Solution1

一开始有点蒙，因为我一直在想，除了相同的思路，然后在添加的时候反向添加，难道还有什么神奇的方法？

**思路相同：**<a href="https://war3cdota.github.io/2017/05/08/102-Binary-Tree-Level-Order-Traversal/">102. Binary Tree Level Order Traversal</a>

这题应该自信一点，相同的思路，反向添加，切记自信！

**Using DFS**

```java
public class BinaryTreeLevelOrderTraversalII{
    //Using DFS
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if(root==null){
            return res;
        }
        levelOrderBottomHelp(res,root,1);
        return res;
    }
    public void levelOrderBottomHelp(List<List<Integer>> res, TreeNode node, int level){
        if(res.size()<level){
            res.add(0,new ArrayList<Integer>());
        }
        res.get(res.size()-level).add(node.val);
        if(node.left!=null){
            levelOrderBottomHelp(res,node.left,level+1);
        }
        if(node.right!=null){
            levelOrderBottomHelp(res,node.right,level+1);
        }
    }
}
```

## Solution2

**Using BFS**

```java
public class BinaryTreeLevelOrderTraversalII2{
    // Using BFS
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if(root==null){
            return res;
        }
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.add(root);
        while(!queue.isEmpty()){
            int length = queue.size();
            List<Integer> list = new ArrayList<Integer>();
            for(int i=0;i<length;i++){
                if(queue.peek().left!=null){
                    queue.add(queue.peek().left);
                }
                if(queue.peek().right!=null){
                    queue.add(queue.peek().right);
                }
                list.add(queue.poll().val);
            }
            res.add(0,list);
        }
        return res;
    }
}
```

# 总结

>这种题目一定要自信的先把能想到的最好的方法做出来，然后再考虑是否还有另类的解法，关键是一定要自信！