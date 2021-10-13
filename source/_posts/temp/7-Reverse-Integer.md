---
title: 7. Reverse Integer
date: 2017-01-08 14:01:22
tags:
- LeetCode-easy
- 位运算
- Boundary Check(边界值检测)
---

Reverse digits of an integer.

**Example1**: x = 123, return 321<br>
**Example2**: x = -123, return -321

<!--more-->

# Solution

## int转换成字符串解决
>时间复杂度 :O(n) ；空间复杂度: O(n)<br/>
>要点在于String转换为int时，如果此时大于int的最大或最小值，会报NumberFormatException：当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常。<br/>
>可以使用异常捕获，将这种错误出现时：return 0;也即就是出现数字越界，返回0。

```java
public class MyReverseInteger{
	public int reverse(int x) {
		int tmp = Math.abs(x);
		StringBuffer sb = new StringBuffer(tmp+"");
		sb.reverse();
		try{
			return (x>0?Integer.parseInt(sb.toString()):-Integer.parseInt(sb.toString()));
		}catch(NumberFormatException e){
			return 0;
		}
	}
}
```

## 取模法
>一个字符占了8位，一个10位数的int值转为String类型占了80位，在空间上开销就很大了。<br/>
>直接对int数值取模并获取模值，并拼接是一个好办法。

```java
public class Solution {
    public int reverse(int x) {
        if(x == Integer.MIN_VALUE)
            return 0;
        int tmp = Math.abs(x);
        long result = 0;
        while(tmp!=0){
            result *= 10;
            result += tmp%10;
            if(result>Integer.MAX_VALUE)
                return 0;
            tmp /= 10;
        }
        return x>0?(int)result:-(int)result;
    }
}
```

## 考察点：<br/>
>1. 负数的取模，应该将负数转为正数，并在返回前将符号加上。<br/>
>2. 边界检测：<br/>
>    a. 使用long类型作为倒叙存储，如果用int类型作为倒叙存储，转换后数字大于int最大值，将会强制抛弃高位。<br/>
>    b. 对于输入数字检测，当为最小值Integer.MIN_VALUE，Math.abs()函不会去掉负号，应该直接返回0。

