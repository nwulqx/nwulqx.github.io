---
title: 38. Count and Say
date: 2017-04-20 17:13:38
tags:
- LeetCode-easy
- recursion(递归)
- 连续性判断
---
The count-and-say sequence is the sequence of integers beginning as follows:
<font>`1, 11, 21, 1211, 111221, ...`</font>

<font>`1`</font> is read off as <font>`"one 1"`</font> or <font>`11`</font>.<br>
<font>`11`</font> is read off as <font>`"two 1s"`</font> or <font>`21`</font>.<br>
<font>`21`</font> is read off as <font>`"one 2`</font>, then <font>`one 1"`</font> or <font>`1211`</font>.<br>
Given an integer n, generate the nth sequence.<br>

Note: The sequence of integers will be represented as a string.

<style type="text/css">
font{
color:rgb(199,37,78)
}
</style>

<!--more-->

# Solution

>递归思想，要想知道3层，需要知道2层，需要知道1层，了解了按照递归的思路来实现即可！

## 遇到的问题

这题思路很简单，但是实际操作的时候还是遇到了一点问题。在于生成新的字符串时，对于连续的相同的字符进行判断记录。

- 如果当前字符和前一个字符不相等，则应该将当前字符的数量和当前字符添加到新字符串中。

- 如果当前字符和前一个字符相等，则应该将对该字符的计数加一。

- 对于循环的起始应该是从1开始比较好，结束应该是上一次返回的字符串长度加一。

附：

```java
public class Solution {
	public String countAndSay(int n) {
		if(n==1){
			return "1";
		}
		String preStr = countAndSay(n-1);
		StringBuffer sb = new StringBuffer();
		int count = 1;
		for(int i=1;i<preStr.length()+1;i++){
				if(i==preStr.length() || preStr.charAt(i)!=preStr.charAt(i-1)){
				sb.append(count).append(preStr.charAt(i-1));
				count = 1;
			}else{
				count++;
				continue;
			}
		}
		return sb.toString();
	}
}
```

# 总结

>这类题需要快速定位到递归的思路，这种层层相扣的，当前结果需要上次的结果作为输入的问题。在一定程度上使用递归效果很不错。另外对于连续性问题的判断，这种循环的解决技巧也应该谨记！