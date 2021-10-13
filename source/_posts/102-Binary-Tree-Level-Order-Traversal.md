---
title: 102. Binary Tree Level Order Traversal
date: 2017-05-08 15:51:29
tags:
- LeetCode-medium
- recursion(递归)
- Queue(队列)
- Optimize(优化)
- BFS(广度优先遍历)
- DFS(深度优先遍历)
---
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

**For example:**

Given binary tree `[3,9,20,null,null,15,7]`

		    3
		   / \
		  9  20
		    /  \
		   15   7

return its level order traversal as:

		[
		  [3],
		  [9,20],
		  [15,7]
		]

<!-- more -->

# 分析

## BFS队列思路

**javascript**

```js
/*
 * app:leetcode lang:**javascript**
 * https://leetcode.com/problems/binary-tree-level-order-traversal/submissions/
 * Runtime: 105 ms, faster than 28.47%
 * Memory Usage: 40.5 MB, less than 59.99% 
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
 * @return {number[][]}
 */
var levelOrder = function(root) {
    const res = [];
    if(!root) return res;
    const q = [];
    q.push(root);
     // 注意要写大于0
    while(q.length > 0){
        const len = q.length;
        const level = [];
        for(let i = 0; i < len; i++){
            const node = q.shift();
            level.push(node.val);
            if(node.left) q.push(node.left);
            if(node.right) q.push(node.right);
        }
        res.push([...level]);
    }
    return res;
};
```

**c++**

```c++
/*
 * app:leetcode lang:**c++**
 * https://leetcode.com/problems/binary-tree-level-order-traversal/submissions/
 * Runtime: 0 ms, faster than 100.00 %
 * Memory Usage: 12.4 MB, less than 84.74 %
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            int size = q.size();
            vector<int> level(size);
            for(int i = 0; i < size; i++){
                TreeNode* node = q.front();
                q.pop();
                level[i] = node->val;
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
            }
            res.push_back(level);
        }
        return res;
    }
};
```



## Solution1

我觉得第一想法很重要，因为第一思路体现了你所学的和所知道的东西。

```java
public class BinaryTreeLevelOrderTraversal{
    static List<List<Integer>> reslist = null;
    public List<List<Integer>> levelOrder(TreeNode root) {
        reslist = new ArrayList<List<Integer>>();
        if(root==null){
            return reslist;
        }
        List<TreeNode> nodeList = new ArrayList<TreeNode>();
        List<Integer> levelList = new ArrayList<Integer>();
        nodeList.add(root);
        levelList.add(root.val);
        reslist.add(levelList);
        levelOrderHelp(nodeList);
        return reslist;
    }
    public void levelOrderHelp(List<TreeNode> list){
        List<Integer> levelList = new ArrayList<Integer>();
        List<TreeNode> nodeList = new ArrayList<TreeNode>();
        for(TreeNode node:list){
            if(node.left!=null){
                nodeList.add(node.left);
                levelList.add(node.left.val);
            }
            if(node.right!=null){
                nodeList.add(node.right);
                levelList.add(node.right.val);
            }
        }
        if(nodeList.size()==0){
            return ;
        }
        reslist.add(levelList);
        levelOrderHelp(nodeList);
    }
}
```

这解法是我第一想法，在最短的时间内我所得到的AC思路。应该值得去优化下，我第一想法，想到了利用递归；但是有很多地方是做的很冗余的，对于遍历二叉树和存储二叉树节点的值，我使用了两个数组。

## 优化

## Solution2

**DFS思路**

减少数组的使用，使用DFS深度优先遍历+递归

```java
public class BinaryTreeLevelOrderTraversal{
    // Using DFS recursion !
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> reslist = new ArrayList<List<Integer>>();
        if(root==null){
            return reslist;
        }
        levelOrderHelp(reslist,root,1);
        return reslist;
    }
    public void levelOrderHelp(List<List<Integer>> reslist, TreeNode node, int level){
        if(reslist.size()<level){
            reslist.add(new ArrayList<Integer>());
        }
        reslist.get(level-1).add(node.val);
        if(node.left!=null){
            levelOrderHelp(reslist,node.left,level+1);
        }
        if(node.right!=null){
            levelOrderHelp(reslist,node.right,level+1);
        }
    }
}
```

>使用DFS的思路，对于二叉树上的每一个节点，根据传进去的level参数，在数组中找到它的定位并添加。

## Solution3

**BFS思路**

```java
public class BinaryTreeLevelOrderTraversal{
    // Using BFS
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> reslist = new ArrayList<List<Integer>>();
        if(root==null){
            return reslist;
        }
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.add(root);
        while(!queue.isEmpty()){
            int length = queue.size();
            List<Integer> list = new ArrayList<Integer>();
            for(int i=0;i<length;i++){
                TreeNode node = queue.poll();
                list.add(node.val);
                if(node.left!=null){
                    queue.add(node.left);
                }
                if(node.right!=null){
                    queue.add(node.right);
                }
            }
            reslist.add(list);
        }
        return reslist;
    }
}
```
>主要思路是利用Queus队列这一数据结构，来实现BFS遍历。

# 总结
>这个题很不错，总结了前面的二叉树的各种使用方法，最后灵活的解决了问题。注意使用递归和Queue和Stack这几种数据机构和方法，这些是解决二叉树问题的基本手段。