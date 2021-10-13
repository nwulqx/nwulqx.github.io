---
title: 3. Longest Substring Without Repeating Characters
date: 2017-02-10 11:14:13
tags:
- LeetCode-medium
- 快慢指针
- Optimize(优化)
---

Given a string, find the length of the longest substring without repeating characters.

**Examples:**

Given <font>`"abcabcbb"`</font>, the answer is <font>`"abc"`</font>, which the length is 3.

Given <font>`"bbbbb"`</font>, the answer is <font>`"b"`</font>, with the length of 1.

Given <font>`"pwwkew"`</font>, the answer is <font>`"wke"`</font>, with the length of 3. Note that the answer must be a substring, <font>`"pwke"`</font> is a *subsequence* and not a **substring**.

<style type="text/css">
font{
color:rgb(199,37,78)
}
</style>

<!--more-->

# Solution

>求最长不重复序列。

## 循环比对

>对于所有可能的情况进行比较，找到最长的不重复子序列并保存长度。

```java
public int lengthOfLongestSubstring(String s) {
	if(s.length()==0)
		return 0;
	int len = 0,i = 0;
	while(i<s.length()){
		int j = i+1;
		while(j<s.length()){
			if(s.substring(i,j).contains(String.valueOf(s.charAt(j))))
				break;
			j++;
		}
		if((j-i)>len)
			len = j-i;
		i++;
	}
	return len;
}
```
`s.substring(i,j).contains(String.valueOf(s.charAt(j)))`这个判断完成了核心的逻辑判断。

## HashMap

**分析**

这个方法我觉得并没有多少优势，使用下面HashSet方法表述的方法更清晰。

>The basic idea is, keep a hashmap which stores the characters in string as keys and their positions as values, and keep two pointers which define the max substring. move the right pointer to scan through the string , and meanwhile update the hashmap. If the character is already in the hashmap, then move the left pointer to the right of the same character last found. Note that the two pointers can only move forward.

>使用Map来存储，`字符-索引`；<br>
>两个索引：低索引和高索引，默认值为0<br>
>当高索引遍历到重复字符时，低索引将移动到重复字符第一次出现的位置+1（但是有一定很重要，低索引只能增不能减），那么现在高索引处的字符在`低索引---高索引`组成的子字符串是唯一的。<br>
>每次在比较并存储在最长的子序列。

```java
import java.util.*;
public class LongestSubstringWithoutRepeatingCharacters{
	//HashMap   This method is very obscure!
    public static int lengthOfLongestSubstring(String s) {
    	if(s.length()==0)
    		return 0;
    	int max = 0;
    	Map<Character,Integer> map = new HashMap<>();
    	for(int i=0,j=0;i<s.length();i++){
    		if(map.containsKey(s.charAt(i))){
    			//Note that the two pointers can only move forward.
    			j = Math.max(j,map.get(s.charAt(i))+1);
    			// j = map.get(s.charAt(i))+1;
    			System.out.println("j="+j);
    		}
    		map.put(s.charAt(i),i);
    		max = Math.max(max,i-j+1);
    	}
    	return max;
    }
}
```
**分析：**

![](http://i.imgur.com/aZO47aN.png)

## HashSet

**快慢指针法**

>使用快慢指针来解决这个问题，快指针用来添加不存在的字符；而当存在重复字符时，慢指针的作用是用来从字符串的头部删除字符，直到重复的字符被删除为止。

```java
import java.util.*;
public class LongestSubstringWithoutRepeatingCharacters{
	//HashSet
    public static int lengthOfLongestSubstring(String s) {
    	if(s.length()==0)
    		return 0;
    	Set<Character> set = new HashSet<Character>();
    	int i = 0, j = 0,max = 0;
    	while(j<s.length()){
    		if(!set.contains(s.charAt(j))){
    			set.add(s.charAt(j++));
    			max = Math.max(max,set.size());
    		}else
    			set.remove(s.charAt(i++));
    	}
    	return max;
    }
}
```
**分析：**

>利用了快慢指针来解决这个问题，没有重复元素时，快指针用来添加不存在字符；反之，慢指针用来删除头字符。<br>
>这样做的好处是利用快慢指针可以快速的得到所有可能的不重复子串。

# 总结

>最简单易懂的方法是使用循环遍历出所有可能的结果，并筛选出最长的子字符串。时间复杂度达到了O(N2)<br>
>使用HashMap或者HashSet简化时间复杂度到O(N)。