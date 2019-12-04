---
title: 66. Plus One
date: 2017-04-24 16:29:33
tags:
- LeetCode-easy
- 位运算
---
Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.

<!--more-->

# Solution

## 分析

其实，仔细看这道题，进位运算是这道题的考点。何时进位，如何进位，以及连续的进位应该怎么做？

**伪码**

	for(i<--digits[digits的长度-1];i>=0;i--){
	    if(digits[i]<9){//这里很巧妙，小于9，则直接+1后return，如果能想到这里的话，基本上就很简单了
	        digits[i]++;
	        return digits;
	    }else{
	        digits[i] = 0;//这里其实只需要置0即可，因为这里最大的进位仅为1，所以不需要考虑大于1的进位
	    }
	}
	newDigits数组 <-- 新数组[digits的长度+1]//到达了这一步仍没有返回，说明，每一位都是9，所以，出现了比原数组多了一位。
	newDigits[0] <-- 1;
	return newDigits;

**源码**

```java
public class PlusOne{
    public static int[] plusOne(int[] digits) {
        if(digits.length == 0)
            return digits;
        int i = digits.length-1;
        while(i>=0){
            if(digits[i]<9){
                digits[i]++;
                return digits;
            }else{
                digits[i] = 0;
                i--;
            }
        }
        int []newDigits = new int[digits.length+1];
        newDigits[0] = 1;
        return newDigits;
    }
}
```

```java
public static int[] plusOne(int[] digits) {
    for(int i=digits.length-1;i>=0;i--){
        if(digits[i]<9){
            digits[i]++;
            return digits;
        }else{
            digits[i]=0;
        }
    }
    int newDigits = new int[digits.length+1];
    newDigits[0] = 1;
    return newDigits;
}
```

## 思考

>这道题其实对我来说很难。对于进位运算的操作和实践太少，思路也不够清晰。<br>
>主要思路在于，对于位上是9的操作，只需要将该位置0，而对于位上小于9的操作，只需要该位加1，返回即可。这是加1运算的局限，不需要单独的进位变量，因为进位最大不会超过1。

# 总结

>进位运算其实很考察逻辑，需要注意的是进位。