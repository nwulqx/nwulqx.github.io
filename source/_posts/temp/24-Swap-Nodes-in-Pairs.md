---
title: 24. Swap Nodes in Pairs
date: 2017-03-07 10:52:56
tags:
- LeetCode-easy
- recursion(递归)
- LinkedList(链表)
---

Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given <font color='rgb(199,37,78)'>`1->2->3->4`</font>, you should return the list as <font color='rgb(199,37,78)'>`2->1->4->3`</font>.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

<!--more-->

# Solution：

## 循环解决

> 先明确链表元素交换，这样就好做了！

![](http://i.imgur.com/Yxya3WY.png)

### 思路

>1. 通过temp节点获取first和second的索引，并且交换两个元素；
>2. 重新获取temp元素，并重复步骤1。

```java
public ListNode swapPairs(ListNode head) {
	ListNode node = new ListNode(9527);
	node.next = head;
	ListNode temp = node;
	while(temp.next!=null && temp.next.next!=null){
		ListNode first = temp.next;
		ListNode second = temp.next.next;
		first.next = second.next;
		second.next = first;
		temp.next = second;
		temp = first;
	}
	return node;
}
class ListNode {
     int val;
     ListNode next;
     ListNode(int x) { val = x; }
}
```

## 递归解决

![](http://i.imgur.com/O2rttX2.png)

>利用递归的思路解决，把一次操作封装成函数，借助递归实现。

```java
//recursion: the recursive stack uses O(n) space
public ListNode swapPairs(ListNode head) {
	if(head == null || head.next == null)
		return head;
	ListNode node = head.next;
	head.next = swapPairs(node.next);
	node.next = head;
	return node;
}

class ListNode {
     int val;
     ListNode next;
     ListNode(int x) { val = x; }
}
```

