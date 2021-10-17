---
title: 145. Binary Tree Postorder Traversal
date: 2017-05-19 18:20:56
tags:
- LeetCode-easy
- recursion(递归)
- Post-Order Traversal(后序遍历)
- Morris Traversal
---
Given a binary tree, return the postorder traversal of its nodes' values.

For example:
Given binary tree `{1,#,2,3}`,

       1
        \
         2
        /
       3

return `[3,2,1]`.

**Note**: Recursive solution is trivial, could you do it iteratively?

<!-- more -->

# Solution

## Solution1

**使用递归(Recursion)**

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/binary-tree-postorder-traversal/
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 8.5 MB, less than 63.43%
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
private:
    vector<int> res;
public:
    vector<int> postorderTraversal(TreeNode* root) {
        postorder(root);
        return res;
    }
    void postorder(TreeNode* node){
        if(node == NULL) return;
        res.push_back(node->val);
        postorder(node->left);
        postorder(node->right);
    }
};
```



**java**

```java
public class BinaryTreePostorderTraversal{
    // Using recursion！
    public List<Integer> postorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        postorderHelper(list,root);
        return list;
    }
    public void postorderHelper(ArrayList<Integer> list, TreeNode node){
        if(node==null){
            return;
        }
        postorderHelper(list,node.left);
        postorderHelper(list,node.right);
        list.add(node.val);
    }
}
public class TreeNode {
 int val;
 TreeNode left;
 TreeNode right;
 TreeNode(int x) { val = x; }
}
```

## Solution2

**不使用递归(Without using recursion)**

>对于[1,2,3,4,5]

		     1
		    / \
		   2   3
		  / \   
		 4   5

我们发现，有后序遍历[4,5,2,3,1]，它的反转[1,3,2,5,4]，是一个遍历先右子树的先序遍历。那么就可以参考先序遍历的思路来解决！

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/binary-tree-postorder-traversal/
 * Runtime: 80 ms, faster than 41.12%
 * Memory Usage: 39.2 MB, less than 11.72%
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
 * @return {number[]}
 */
var postorderTraversal = function(root) {
    const st = [];
    const res = [];
    let pre = null;
    while(root || st.length > 0){
        if(root){
            st.push(root);
            root = root.left;
        }else{
            let node = st[st.length-1];
            if(node.right && node.right !== pre){
                root = node.right;
            }else{
                res.push(node.val);
                pre = node;
                st.pop();
            }
        }
    }
    return res;
};
```



**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/binary-tree-postorder-traversal/
 * Runtime: 4 ms, faster than 43.99%
 * Memory Usage: 8.3 MB, less than 86.67%
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
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        if(!root) return res;
        stack<TreeNode*> st;
        TreeNode* pre = NULL;
        while(root || !st.empty()){
            if(root){
                st.push(root);
                root = root->left;
            }else{
                TreeNode* node = st.top();
                if(node->right && pre != node->right){
                    root = node->right;
                }else{
                    res.push_back(node->val);
                    pre = node;
                    st.pop();
                }
            }
        }
        return res;
    }
};
```



**java**

```java
/*for [1,2,3,4,5]
         1
        / \
       2   3
      / \   
     4   5
    We have [4,5,2,3,1]  --->  [1,3,2,5,4]
    It is the reverse of mid-->right-->left !
    So we can refer to the Binary Tree Preorder Traversal !
*/
public class BinaryTreePostorderTraversal{
    public List<Integer> postorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode node = root;
        while(node!=null || !stack.empty()){
            if(node!=null){
                stack.push(node);
                list.add(0,node.val);
                node = node.right;
            }else{
                TreeNode p = stack.pop();
                node = p.left;
            }
        }
        return list;
    }
}
```

## Solution3

**不使用递归(Without using recursion)**

```java
public class BinaryTreePostorderTraversal{
    public List<Integer> postorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode node = root;
        while(node!=null){
            list.add(0,node.val);
            if(node.left!=null){
                stack.push(node.left);
            }
            node = node.right;
            if(node==null && !stack.empty()){
                node = stack.pop();
            }
        }
        return list;
    }
}
```

## Solution4

**不使用递归(Without using recursion)**

>上面两种非递归的实现，大同小异，注意写法即可。但是上面的涉及一个思路，上面两种解法是基于先序遍历的思路，逆向过来的。而不是真正意义上的从上至下的遍历。要想从上至下的判断，需要考虑一个问题，因为根节点会在左孩子被访问后，再访问，但是，此时如果右孩子节点未被访问，则先访问右孩子节点。这里的判断需要注意。

```java
public class BinaryTreePostorderTraversal{
    public List<Integer> postorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode node  = root,pre = null;
        while(node!=null || !stack.empty()){
            if(node!=null){
                stack.push(node);
                node = node.left;
            }else{
                TreeNode p = stack.peek();
                if(p.right!=null && p.right!=pre){
                    node = p.right;
                    continue;
                }
                pre = p;
                list.add(p.val);
                stack.pop();
                node = null;
            }
        }
        return list;
    }
}
```
>参数pre不是很好理解，它的意义在于，防止避免造成向下访问的死循环，告知该节点已访问。

>这里修改了了<a href="https://war3cdota.github.io/2017/05/19/112-Path-Sum/">112. Path Sum</a>后序遍历解法得到。

## Solution5

**Morris traversal**

>时间复杂度：O(n)
>空间复杂度：O(1)

```java
public class BinaryTreePostorderTraversal2{
    // Morris Traversal !
    public List<Integer> postorderTraversal(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        TreeNode cur = root;
        while(cur!=null){
            if(cur.right==null){
                list.add(0,cur.val);
                cur = cur.left;
            }else{
                TreeNode pre = cur.right;
                while(pre.left!=null && pre.left!=cur){
                    pre = pre.left;
                }
                if(pre.left==null){
                    list.add(0,cur.val);
                    pre.left = cur;
                    cur = cur.right;
                }else{
                    pre.left = null;
                    cur = cur.left;
                }
            }
        }
        return list;
    }
}
```

# 总结

>后序遍历的非递归思路有两种：
> 1. 根据先序遍历，利用数据结构，使用先序遍历的相同方法可以解决。
> 2. 自上向下的遍历，但是可能在是否访问过该节点需要再做判断。
> 3. 后序遍历的Morris Traversal借助先序遍历的思路。