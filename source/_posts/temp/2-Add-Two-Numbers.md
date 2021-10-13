---
title: 2. Add Two Numbers
date: 2017-02-08 11:17:16
tags:
- LeetCode-medium
- Optimize(优化)
- 位运算
- LinkedList(链表)
---

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a `single digit`. Add the two numbers and return it as a linked list.

**Input**: (2 -> 4 -> 3) + (5 -> 6 -> 4)<br>
**Output**: 7 -> 0 -> 8

<!--more-->

# Solution

## 分析

>1. 每一个节点上都包含一个单个的数字，那么也就是说进位值最多为1；
>
>2. 结尾处如果存在进位，则应该新建节点。
>

**版本一**

```java
public class Add2Numbers{
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode digit_1 = l1;
        ListNode digit_2 = l2;
        ListNode p = new ListNode(0);
        ListNode sum = new ListNode(0);
        p.next = sum;
        
        int carry = 0;
        
        while(digit_1 != null || digit_2 != null){
            int addUp = (digit_1 != null ? digit_1.val : 0) + (digit_2 != null ? digit_2.val : 0) + carry;
            sum.next = (carry = addUp / 10) == 0 ? new ListNode(addUp) : new ListNode(addUp % 10);
            if(digit_1 != null)
                digit_1 = digit_1.next;
            if(digit_2 != null)
                digit_2 = digit_2.next;
            sum = sum.next;
        }
        
        if(carry > 0){
            sum.next = new ListNode(carry);
        }
        
        return p.next.next;
    }
}
```

## 优化

```java
public class Add2Numbers{
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode c1 = l1;
        ListNode c2 = l2;
        ListNode d = new ListNode(0);
        ListNode result = d;
        int sum = 0;
        while(c1!=null || c2!=null){
            //we need sum/10  
            sum /= 10;
            if(c1!=null){
                sum += c1.val;
                c1 = c1.next;
            }
            if(c2!=null){
                sum += c2.val;
                c2 = c2.next;
            }
            //① very clever!
            d.next = new ListNode(sum%10);
            d = d.next;
        }
        //②if we have carry
        if(sum/10==1)
            d.next = new ListNode(1);
        return result.next;
    }
}
class ListNode{
    int val;
    public ListNode(int val){
        this.val = val;
    }
    ListNode next;
}
```
>① 处直接取模，不需要判断，因为你需要个位上的数字，那么无论数字大于还是小于10都可以取模得到个位上的数字。

>② 处是对结尾处进位进行判断，由于每一位最大为9，所以结尾处只需判断是否需要进位，需要进位1即可。

# Summary

>这道题主要考察了进位运算在链表的使用情况，难点在代码优化。如何写出简洁、高效的算法是目标。而不能局限于问题的解决！