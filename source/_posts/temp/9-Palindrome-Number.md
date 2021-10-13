---
title: 9. Palindrome Number
date: 2017-01-10 19:14:09
tags:
- LeetCode-easy
- Boundary Check(边界值检测)
- Optimize(优化)
---
Determine whether an integer is a palindrome. Do this without extra space.

<!--more-->

# Solution

## 简单的字符串比较

>借助StringBuffer函数的reverse()方法，可以轻松的对字符串反转，在对翻转后的数字和原数字比较，相等则为回文数。

### 出现的问题：

>1. 数字越界问题，通过stringbuffer转换后，可能出现转化后的数字超越了int的范围。
>2. 这样做的时间复杂度和空间复杂度是很浪费的，一个字符是占8位，10位数将占到80位，大于int的32位。

## 直接操作int

>使用取模操作直接操作int数字，相等即为回文数。

### Optimized

>不需要全部转化，只需要转化一半数字即可。但是，由于位数的奇偶性质，可能会出现：
>
>1. 左右相等；
>2. 左右不相等。
	
	12321转化一般得到12 和 123；
	1221 转化则得到12 和 12。

>**解决办法**：同时检查，（左==右） || （左/10 == 右）。

## Boundary Check
1. 负数都不是回文数
2. 0是回文数，但是`int%0 == 0` 的数不是回文数，但如果采用优化的方案。例如1000，得到的对应的判断是0 和 10，会被误判断为true。

```java
public class PalindromeNumber{
	public static void main(String args[]){
		System.out.println(isPalindrome(20));
	}
	public static boolean isPalindrome(int x) {
		if(x<0||(x!=0 && x%10==0)) return false;
		int result = 0;
		while(x>result){
			result*=10;
			result+=(x%10);
			x/=10;
		}
		return (x==result || x==result/10);
    }
}
```
# 总结

>这个题从优化和边界检测两个地方考察。