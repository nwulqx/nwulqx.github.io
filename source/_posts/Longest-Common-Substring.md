---
title: Longest Common Substring
date: 2017-01-22 17:45:25
tags:
- LeetCode-easy
- DP(动态规划)
- Optimize(优化)
---

Write a function to find the longest common substring amongst two strings.

<!--more-->

# Solution

## 循环查找

>思路：

>1. 双循环嵌套，对两个字符串每一个字符进行对比；
>2. 如果相同，则应该继续比较，找到当前索引开始的最长相同字符串长度；
>3. 每次找到的相同字符串并不一定是最长的，所以需要再做一次比较，保存最长的子串的索引。

时间复杂度：O(n2)
```java
public class LongestCommonSubstring{
	public static String longestCommonSubstring(String str1,String str2){
		int len1 = str1.length();
		int len2 = str2.length();
		int start = 0, len = 0;
		for(int i=0;i<len1;i++){
			for(int j=0;j<len2;j++){
				if(str1.charAt(i)!=str2.charAt(j))
					break;
				int start1 = i+1,start2 = j+1,length = 1;
				while(start1<len1 && start2<len2){
					if(str1.charAt(start1)==str2.charAt(start2)){
						start1++;
						start2++;
						length++;
					}else
						break;
				}
				if(length>len){
					start = start1-length;
					len = length;
				}
			}
		}
		return str1.substring(start,start+len);
	}
}
```

# DP问题

>转换成DP问题，当前字串满足最长子串的前提是字串(n-1)满足最长子串&&当前字符相等。<br>
>   动态转移方程为：

   	如果xi == yj， 则 c[i][j] = c[i-1][j-1]+1

   	如果xi ! = yj,  那么c[i][j] = 0

时间复杂度：O(n2)

```java
public class LongestCommonSubstring3{
	public static void main(String []args){
		System.out.println(
			longestCommonSubstring("","saabcs"));
	}
	public static String longestCommonSubstring(String str1,String str2){
		int len1 = str1.length()+1;
		int len2 = str2.length()+1;
		int r[][] = new int[len1][len2];
		for(int m=0;m<len1;m++)
			r[m][0] = 0;
		for(int n=0;n<len2;n++)
			r[0][n] = 0;
		int start = 0,length = 0;
		for(int i=1;i<len1;i++){
			for(int j=1;j<len2;j++){
				if(str1.charAt(i-1)==(str2.charAt(j-1)))
					r[i][j] = r[i-1][j-1]+1;
				if(r[i][j] > length){
					start = i-length-1;
					length = r[i][j];
				}
			}
		}
		return str1.substring(start,start+length);
	}
}
```

# 总结

练习下动态规划的思路！