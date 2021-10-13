---
title: 6. ZigZag Conversion
date: 2017-01-06 16:51:28
tags:
- LeetCode-easy
- 嵌套指针
---

The string <font color='rgb(199,37,78)'>"PAYPALISHIRING"</font> is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

	P   A   H   N
	A P L S I I G
	Y   I   R

And then read line by line: <font color='rgb(199,37,78)'>"PAHNAPLSIIGYIR"</font>

Write the code that will take a string and make this conversion given a number of rows:

	string convert(string text, int nRows);

<font color='rgb(199,37,78)'>convert("PAYPALISHIRING", 3)</font> should return <font color='rgb(199,37,78)'>"PAHNAPLSIIGYIR"</font>.

<!--more-->

# Brute Force：
>生成numRows个StringBuffer对象;<br>
>从0~n-1循环添加元素共n个，再从n-2到1循环添加元素共n-2个；<br>
>外层使用while循环，自增通过索引内 i++。

```java
while(i<str.length){
	for(int j=0;j<numRows&&i<str.length;j++)
		sb[j].append(str[i++]);
	
	for(int k=numRows-2;k>0&&i<str.length;k--)
		sb[k].append(str[i++]);
}
```
时间复杂度是O(n)。

```java
public class Solution {
    public String convert(String s, int numRows) {
        char c[] = s.toCharArray();
        StringBuffer sb[] = new StringBuffer[numRows];
        for(int j=0;j<sb.length;j++)
            sb[j] = new StringBuffer();
        int low = 0;
        while(low < c.length){
            for(int i=0;i<numRows && low<c.length;i++)
                sb[i].append(c[low++]);
            for(int j=numRows-2;j>0 && low<c.length;j--)
                sb[j].append(c[low++]);
        }
        for(int i=1;i<sb.length;i++)
            sb[0].append(sb[i]);
        return sb[0].toString();
    }
}
```

# 嵌套指针法：
>该方法的精髓在于：建立新的数组存储每一个元素对应的新数组的索引（需要先建立numRows个StringBuffer对象）

	/*n=numRows
	Δ=2n-2    0                           2n-2                       4n-4
	Δ=        1                     2n-3  2n-1                4n-5   4n-3
	Δ=        2               2n-4        2n              4n-4       .
	Δ=        .           .               .               .            .
	Δ=        .       n+1                 .           3n+1              .
	Δ=        n-2 n                       3n-4    3n                 5n-6
	Δ=2n-2    n-1                         3n-3                       5n-5
	*/

其时间复杂度为O(n)。

核心算法：

```java
index[i] = i%(2*numRows-2);
if(index[i]>(numRows-1))
	index[i] = (2*numRows-2)-index[i];

0     6
1  5  7
2  4  8
3     9
```

>每6个数为一个循环，可知模数`2n-2`<br>
>但是，斜着上去的那一行算出了`补数`，需要用模数去减它才可以得到正确的行数。

找规律：2*n-2，n指一列的长度。 

```java
public class Solution {
    public String convert(String s, int numRows) {
        if(numRows == 1)
            return s;
        char c[] = s.toCharArray();
        StringBuffer sb[] = new StringBuffer[numRows];
        for(int i=0;i<sb.length;i++)
            sb[i] = new StringBuffer();
        int index[] = new int[c.length];
        for(int i=0;i<c.length;i++){
            index[i] = i % (2*numRows-2);
            if(index[i]>numRows-1)
                index[i] = 2*numRows-2 - index[i];
        }
        for(int j=0;j<c.length;j++)
            sb[index[j]].append(c[j]);
        for(int k=1;k<sb.length;k++)
            sb[0].append(sb[k]);
        return sb[0].toString();
    }
}
```

## Boundary Check

>嵌套指针会遇到一个异常，除零异常。那么，应该检测`numRows`值是否为`1`，如果为`1`，则应该直接返回字符串`s`。

# 总结

>1. 这道题直接去解，是一个好方法，但是明显是一个索引递增的循环。
>2. 嵌套指针的使用可以更巧妙的解决这道题目，至于巧在哪里？比直接循环好在，封装了每行的索引生成，通过列高可以计算出每个元素相应的行索引。