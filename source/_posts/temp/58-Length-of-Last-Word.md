---
title: 58. Length of Last Word
date: 2017-04-21 17:16:37
tags:
- LeetCode-easy
---
Given a string s consists of upper/lower-case alphabets and empty space characters `' '`, return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example,
Given s = `"Hello World"`,
return `5`.

<!--more-->

# Solution

## Solution1

**伪码**

	inputString <-- 输入字符串消去前后多余的空白字符
	wordsArray[] <-- inputString按照空格" "分割成字符串数组
	if wordsArray的长度 == 0
	return 0
	else
	return 数组最后元素的长度

**Java源码**

```java
public class LengthofLastWord{
	public int lengthOfLastWord(String s) {
		String inString = s.trim();
		String wordsArray[] = inString.split(" ");
		return wordsArray.length==0?0:wordsArray[wordsArray.length-1].length();
	}
}
```

## Solution2

方法一操作过于复杂，不如直接操作字符效率高。

**伪码**

	inputString <-- 输入字符串消去前后多余的空白字符
	设置计数length <-- 0
	for(i<--inputString的长度;i>=0;i--){
		if(inputString在i处索引的字符不是空字符' '){
			length++;
		}else{
			跳出循环
		}
	}
	return length

**Java源码**

```java
public class LengthofLastWord{
	public int lengthOfLastWord(String s) {
	String inString = s.trim();
	int length = 0;
	for(int i=inString.length()-1;i>=0;i--){
		if(inString.charAt(i)!=' '){
			length++;
		}else{
			break;
		}
	}
	return length;
	}
}
```

# 总结

>easy题，过！先看下有没有叼一点其他解法。OK~~有个写法比我吊的。

```java
public int lengthOfLastWord(String s) {
	return s.trim().length()-s.trim().lastIndexOf(" ")-1;
}
```

>其他思路：

```java
public int lengthOfLastWord(String s) {
	s = s.trim();
	int lastIndex = s.lastIndexOf(' ') + 1;
	return s.length() - lastIndex;
}
```

>好了，不要讨论难易了，简单题更应该多看看多解性！