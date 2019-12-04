---
title: 83. Remove Duplicates from Sorted List
date: 2017-04-27 17:00:05
tags:
- LeetCode-easy
- Optimize(优化)
- recursion(递归)
- LinkedList(链表)
---
Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,<br>
Given `1->1->2`, return `1->2`.<br>
Given `1->1->2->3->3`, return `1->2->3`.

<!-- more -->
# Solution

## Solution1

**伪码**

	while(head的下一个节点 != null){
	    second <-- head的下一个节点
	    if(second的值 == head的值){
	        third <-- second的下一个节点
	        if(third != null){
	            second的值 <-- third的值
	            second的下一个节点 <-- third的下一个节点
	        }else{
	            head的下一个节点 <-- null
	        }
	    }else{
	        head <-- head的下一个节点
	    }
	}

这里用了最简单的思路：

>当前节点如果和下一个节点的值相等，则删除下一个节点（如何删除下一个节点，则应该判断下下一个节点的下一个节点是否为null），同时指针不向后遍历。
>如果不等，则遍历下一个节点。

```java
public class RemoveDuplicatesfromSortedList{
    public ListNode deleteDuplicates1(ListNode head) {
        if(head==null){
            return head;
        }
        ListNode first = head;
        while(first.next!=null){
            ListNode second = first.next;
            if(second.val == first.val){
                ListNode third = second.next;
                if(third!=null){
                    second.val = third.val;
                    second.next = third.next;
                }else{
                    /*
                    Err : second = null;//Only pont second is null;
                    We need first.next = null;
                    */
                    first.next = null;
                    break;
                }
            }else{
                first = first.next;
            }
        }
        return head;
    }
}
```

**优化**
上述的方法其实太过复杂了，应该是可以优化的。我从`first.next!=null`作为的循环判断条件。最好的话，其实使用head != null是最快捷的。

## Solution3

**源码**

```java
public class RemoveDuplicatesfromSortedList{
    public ListNode deleteDuplicates2(ListNode head) {
        if(head == null){
            return head;
        }
        ListNode preNode = new ListNode(9527);
        preNode.next = head;
        while(head!=null){
            if(head.next!=null && head.val == head.next.val){
                head.next = head.next.next;
            }else{
                head = head.next;
            }
        }
        return preNode.next;
    }
}
```
## 更好的方法

采用递归，便于阅读以及理解。

```java
public class RemoveDuplicatesfromSortedList{
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null || head.next==null){
            return head;
        }
        head.next = deleteDuplicates(head.next);
        return head.val == head.next.val?head.next:head;
    }
}
```

**代码感悟**

>其实挺想写一下这个递归思路的，看了这个递归，其实是尾递归的一种，一开始上去确实还不太会写。主要分为3步：

>1. 边界判断，如果head为null或者head没有后面的节点，则直接返回head;<br>
>2. head的下一个节点是递归调用这个函数的返回值。这里有说法，如果函数走到这里，倒数3个三个节点已经确定了！因为最后一个节点为null，倒数第一个节点只有一个，倒数第二个节点现在的下一个节点指向了倒数第一个节点;<br>
>3. 递归的核心，函数返回值，判断当前节点和下一个节点的值是否相等，以此来决定返回值。<br>
这种尾递归的操作，感觉还是挺值得思考的！

# 总结

>这道题使用各种方法都可以解决，关键是解决的思路有所不同。第一种是我最先想到的，虽然逻辑上没有问题，但其实，如果采用第二种逻辑上的判断，则代码上会更少，可读性更好。<br>
至于最后一种递归方案，我觉得是我最值得去学习的，很好的思路和方法！