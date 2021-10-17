---
title: 107. Binary Tree Level Order Traversal II
date: 2017-05-08 17:54:47
tags:
- LeetCode-medium
- Tree(树)
- recursion(递归)
- Queue(队列)
- BFS(广度优先遍历)
- DFS(深度优先遍历)
---
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```c++
    3
   / \
  9  20
    /  \
   15   7
```
return its bottom-up level order traversal as:

```c++
	[
	  [15,7],
	  [9,20],
	  [3]
	]
```

<!-- more -->

# Solution

## Solution1

**Using BFS**

**javascript**

```js
/*
 * app:leetcode lang:Javascript
 * https://leetcode.com/problems/binary-tree-level-order-traversal-ii/
 * Runtime: 68 ms, faster than 98.21%
 * Memory Usage: 40.9 MB, less than 15.56% 
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
var levelOrderBottom = function(root) {
    const res = [];
    if(!root) return res;
    const q = [];
    q.push(root);
    while(q.length > 0){
        const len = q.length;
        const level = [];
        for(let i = 0; i < len; i++){
            const node = q.shift();
            level.push(node.val);
            if(node.left) q.push(node.left);
            if(node.right) q.push(node.right);
        }
        res.unshift([...level]);
    }
    return res;
};
```



**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/binary-tree-level-order-traversal-ii/
 * Runtime: 4 ms Beats : 93.18%
 * Memory: 12.6 MB Beats: 88.08%
 */
class Solution {
public:
	vector<vector<int>> levelOrderBottom(TreeNode* root) {
		vector<vector<int>> result;
		if (root == NULL){
			return result;
		}
		queue<TreeNode*> q;
		q.push(root);
		while (!q.empty()){
			int length = q.size();
			vector<int> level;
			while (length--){
				TreeNode* t = q.front();
				q.pop();
				level.push_back(t->val);
				if (t->left != NULL){
					q.push(t->left);
				}
				if (t->right != NULL){
					q.push(t->right);
				}
			}
			result.push_back(level);
		}
		reverse(result.begin(), result.end());
		return result;
	}
};
```



**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/binary-tree-level-order-traversal-ii/
 * Beats : 83.47%
 */
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

## Solution2

一开始有点蒙，因为我一直在想，除了相同的思路，然后在添加的时候反向添加，难道还有什么神奇的方法？

**思路相同：** {% post_link 102-Binary-Tree-Level-Order-Traversal %}

这题应该自信一点，相同的思路，反向添加，切记自信！

**DFS**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/binary-tree-level-order-traversal-ii/
 * Beats : 87.41%
 */
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

# 总结

这种题目一定要自信的先把能想到的最好的方法做出来，然后再考虑是否还有另类的解法，关键是一定要自信！