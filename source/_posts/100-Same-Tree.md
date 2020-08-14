---
title: 100. Same Tree
date: 2017-05-04 15:24:18
tags:
- LeetCode-easy
- Tree(树)
- recursion(递归)
- Stack(栈)
- Queue(队列)
- BFS(广度优先遍历)
- DFS(深度优先遍历)
---

Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

**Example 1:**

```c++
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
```

**Example 2:**

```c++
Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
```

**Example 3:**

```c++
Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false
```

<!-- more -->
# Solution

## Solution1

二叉树的操作，使用递归解决。需要注意边界值检查：

1. 同时为空:true
2. 两树节点不同时为空:false
3. 两树节点值不相同：false
4. 递归两树的左右子树

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/same-tree/
 * Beats : 61.62%;
 */
class Solution {
public:
	bool isSameTree(TreeNode* p, TreeNode* q) {
		if (p == nullptr && q == nullptr) return true;
		if (p == nullptr || q == nullptr) return false;
		if (p->val != q->val) return false;
		return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
	}
};
```

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/same-tree/
 * Beats : 40%;
 */
public class SameTree{
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p==null&&q==null){
            return true;
        }
        if(p == null || q == null){
            return false;
        }
        if(p.val == q.val){
            return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
        }
        return false;
    }
}
```

**Python实现**

```python
# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
class Solution(object):
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """
        if p==None and q==None:
            return True
        if p==None or q==None:
            return False
        if p.val!=q.val:
            return False
        return self.isSameTree(p.left,q.left) and self.isSameTree(p.right,q.right)
```



具体的思路还是一个尾递归的思路，先判断尾部叶节点的元素，然后再向上递归。

## Solution2

**使用BFS广度优先遍历**

>广度优先遍历借助了队列。
>整体的思路是按层遍历，直到结束。

```java
public class SameTree{
    //Using BFS
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p==null&&q==null){
            return true;
        }
        Queue<TreeNode> queue_p = new LinkedList<TreeNode>();
        Queue<TreeNode> queue_q = new LinkedList<TreeNode>();
        queue_p.add(p);
        queue_q.add(q);
        while(!queue_p.isEmpty()&&!queue_q.isEmpty()){
            TreeNode pn = queue_p.poll();
            TreeNode qn = queue_q.poll();
            if(pn.val!=qn.val){
                return false;
            }
            if(pn.right!=null){
                queue_p.add(pn.right);
            }
            if(qn.right!=null){
                queue_q.add(qn.right);
            }
            if(queue_p.size()!=queue_q.size()){
                return false;
            }
            if(pn.left!=null){
                queue_p.add(pn.left);
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

**使用DFS深度优先遍历**

>深度优先遍历借助了栈。
>整体的思路由于栈的先进后出，后进先出的特点，所以，一定会先访问到某一个叶节点再返回。

```java
public class SameTree{
    // Using DFS
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p==null && q==null){
            return true;
        }
        if(p==null || q==null){
            return false;
        }
        Stack<TreeNode> stack_p = new Stack<TreeNode>();
        Stack<TreeNode> stack_q = new Stack<TreeNode>();
        stack_p.push(p);
        stack_q.push(q);
        while(!stack_p.empty()&&!stack_q.empty()){
            TreeNode pn = stack_p.pop();
            TreeNode qn = stack_q.pop();
            if(pn.val!=qn.val){
                return false;
            }
            if(pn.left!=null){
                stack_p.push(pn.left);
            }
            if(qn.left!=null){
                stack_q.push(qn.left);
            }
            if(stack_p.size()!=stack_q.size()){
                return false;
            }
            if(pn.right!=null){
                stack_p.push(pn.right);
            }
            if(qn.right!=null){
                stack_q.push(qn.right);
            }
            if(stack_p.size()!=stack_q.size()){
                return false;
            }
        }
        return stack_p.size()==stack_q.size();
    }
}
```

两种遍历二叉树的方式很不相同，但是归根结底只是使用数据结构的不通，方法和思路是一致的。

# 总结
二叉树的递归操作思路是递归思路的一种，需要去熟悉递归边界，递归式。而使用堆栈及队列的遍历操作则是一种递归的循环思路，注重数据结构的使用。