---
title: 141. Linked List Cycle
date: 2017-06-19 11:26:05
tags:
- LeetCode-easy
- 快慢指针
---
Given a linked list, determine if it has a cycle in it.

Follow up:

Can you solve it without using extra space?

<!-- more -->

# Solution

判断是不是环，可以使用快慢指针法：<br>
1. 要么，指针可以达到尾，说明不是环。<br>
2. 要么，快指针会追到慢指针，说明形成环。<br>

P.S.
>注意使用 `do{}while{}` 循环简化代码。

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head==null || head.next==null){
            return false;
        }
        ListNode lowNode = head;
        ListNode fastNode = head;
        do{
            if(lowNode!=null){
                lowNode = lowNode.next;
            }
            if(lowNode!=null){
                lowNode = lowNode.next;
            }
            if(fastNode!=null){
                fastNode = fastNode.next;
            }
        }while(lowNode!=fastNode);
        return fastNode!=null && lowNode!=null;
    }
}
```

# 总结

>快慢指针的典型用法，用来判断是否为构成了环，同时，也应该记住他的另一个功能，用于查找链表中的中位数。