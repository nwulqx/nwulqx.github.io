---
title: 110. Balanced Binary Tree
date: 2017-05-10 18:04:26
tags:
- LeetCode-easy
- recursion(递归)
- Optimize(优化)
- DFS(深度优先遍历)
- AVL树(平衡二叉树)
---
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

<!-- more -->
# Solution

## Solution1

>基本思路，遍历二叉树，递归算出每一个节点的左右子树高度，比较高度，不满足平衡二叉树，返回false；

**递归解决**

>1. 从根结点开始向下遍历节点；
>2. 对每一个节点所构成的子树进行判断是否为平衡树；
>3. 继续递归该节点的左右节点（这个循环的嵌套值得研究）。

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/balanced-binary-tree/
 * Runtime: 127 ms, faster than 26.56%
 * Memory Usage: 44.9 MB, less than 13.58%
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
var isBalanced = function(root) {
    function depth(node){
        if(!node) return 0;
        return Math.max(depth(node.left),depth(node.right)) + 1;
    }
    if(!root) return true;
    return Math.abs(depth(root.left)-depth(root.right)) <= 1 && isBalanced(root.left) && isBalanced(root.right);
};
```



**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/balanced-binary-tree/
 * Runtime: 29 ms, faster than 8.97%
 * Memory Usage: 21.1 MB, less than 22.66% 
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
    bool isBalanced(TreeNode* root) {
        if(!root) return true;
        return abs(help(root->left)-help(root->right)) <= 1 && isBalanced(root->left)&& isBalanced(root->right);
    }
    int help(TreeNode* node){
        if(!node) return 0;
        return max(help(node->left), help(node->right)) + 1;
    }
};
```

**java**

```java
public class BalancedBinaryTree{
    /*Recursion!*/
    public boolean isBalanced(TreeNode root) {
        if(root==null){
            return true;
        }
        //这里判断了当前节点的平衡，并递归了其左右子树
        return getDepth(root.left)-getDepth(root.right)<=1&&isBalanced(root.left)&&isBalanced(root.right);
    }
    public int getDepth(TreeNode node){
        if(node==null){
            return 0;
        }
        return Math.max(getDepth(node.left),getDepth(node.right))+1;
    }
}
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}
```
>此时，由于需要对每一个节点进行平衡判断，每次都要取深度，那么时间复杂度是O(n)，需要对每一个节点都遍历，则时间复杂度是O(n2)。

## Optimized(优化)

>DFS解决，上面的取深度的方法思路虽然是从底部向上求的每一个节点的深度，但是，真正的判断是从root节点开始向下进行的。<br>
>优化的话，尽可能地在递归到二叉树的底部时添加判断操作。
>判断当前节点构成的子树是否平衡：
>&nbsp;&nbsp;&nbsp;&nbsp;1. 当前节点左右比较，高度差大于1，则不是平衡树。
>&nbsp;&nbsp;&nbsp;&nbsp;2. 如果左子树不是平衡树，则当前节点构成的也一定不是平衡树，右子树也是如此。


## Solution2

```java
public class BalancedBinaryTree3{
    /*Optimized!*/
    public boolean isBalanced(TreeNode root) {
        return isBalancedHelp(root)!=-1;
    }
    public int isBalancedHelp(TreeNode node){
        if(node==null){
            return 0;
        }
        int left = isBalancedHelp(node.left);
        if(left==-1){
            return -1;
        }
        int right = isBalancedHelp(node.right);
        if(right==-1){
            return -1;
        }
        return Math.abs(left-right)<=1?Math.max(left,right)+1:-1;
    }
}
```

>这里面有一点技巧要注意，判断完左子树后，应该立马对左子树的返回值进行判断，因为，如果左右子树只要有一个不是平衡二叉树，则无需进行，直接向上层返回。

# 总结
>这种题目，如果不考虑优化，是很好解决的，遍历所有的节点并对所有节点构成的子树进行平衡判断，但是，时间复杂度太高了。
>优化，只要某节点的左右子树中存在非平衡的树，那么上层则无需在判断，直接向上返回即可。