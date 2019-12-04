---
title: 108. Convert Sorted Array to Binary Search Tree
date: 2017-05-10 13:55:31
tags:
- LeetCode-easy
- recursion(递归)
- Queue(队列)
- 二分法
- Boundary Check(边界值检测)
- BFS(广度优先遍历)
- DFS(深度优先遍历)
---
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

Subscribe to see which companies asked this question

<!-- more -->

# Solution

## Solution1

**递归+二分法**

>这道题的思路主要是二分法，由于是一个BST，所以应该满足：节点的左节点小于根节点，右节点大于根节点。<br>
>所以这道题使用二分法来递归的把每一个节点放到BST中。

```java
public class ConvertSortedArraytoBinarySearchTree{
    public TreeNode sortedArrayToBST(int[] nums) {
        int low = 0;
        int high = nums.length-1;
        return sortedArrayToBST(nums,low,high);
    }
    public TreeNode sortedArrayToBST(int[] nums, int low, int high){
        TreeNode node = null;
        if(low<=high){
            int mid = low + (high-low)/2;
             node = new TreeNode(nums[mid]);
             if(low<=mid-1){
                 node.left = sortedArrayToBST(nums,low,mid-1);
             }
             if(high>=mid+1){
                 node.right = sortedArrayToBST(nums,mid+1,high);
             }
        }
        return node;
    }
}
 public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}
```

## Boundary Check(边界检测)

>二分法的边界检测有点糊涂，没有摸清，这里应该注意。


## Solution2

**非递归解法**

```java
public class ConvertSortedArraytoBinarySearchTree{
    public TreeNode sortedArrayToBST(int[] nums) {
        if ( nums.length == 0 ) { 
            return null; 
        }
        TreeNode head = new TreeNode(0);
        Queue<TreeNode> queue_node = new LinkedList<TreeNode>();
        Queue<Integer> queue_low = new LinkedList<Integer>();
        Queue<Integer> queue_high = new LinkedList<Integer>();
        queue_node.add(head);
        queue_low.add(0);
        queue_high.add(nums.length-1);
        while(!queue_node.isEmpty()){
            TreeNode node = queue_node.poll();
            int low = queue_low.poll();
            int high = queue_high.poll();
            int mid = low + (high-low)/2;
            node.val = nums[mid];
            if(low<=mid-1){
                node.left = new TreeNode(0);
                queue_node.add(node.left);
                queue_low.add(low);
                queue_high.add(mid-1);
            }
            if(high>=mid+1){
                node.right = new TreeNode(0);
                queue_node.add(node.right);
                queue_low.add(mid+1);
                queue_high.add(high);
            }
        }
        return head;
    }
}
```

# 总结

>还是DFS+递归和BFD+Queue的解题思路。二叉树的问题万变不离其宗。