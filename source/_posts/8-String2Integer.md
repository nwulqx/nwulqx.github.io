---
title: 8. String2Integer
date: 2017-01-10 18:35:13
tags:
- LeetCode-easy
- Boundary Check(边界值检测)
---

Implement atoi to convert a string to an integer.

**Hint**: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes**: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

<!--more-->

## 需要考虑：
>1.前面的空格需要去除，从第一个非空数字开始取，一直到第一个非数字字符为止。<br>
>2.int最大最小值的问题需要考虑。

## Boundary Check

1. 当数字超过int范围所报的情况，可以使用比int范围更大的long来解决；
2. 当超过long的范围，应该使用异常检测来解决；
3. **字符串应该被合理的截取，以便可以被正确的转化，即使出现异常，也应该是越界异常。**

>这个题的特殊情况处理起来还是比较麻烦的：

输入 | 输出 | 说明 
------------ | ------------- | ------------- |
"   -123abc" | -123 | 过滤空格和非数字 |
"+-123abc" | 0 | 对于多符号数截取了空字符串 |
"+-" | 0 | 同上，返回了空字符串 |
"2147483648" | 2147483647 | 超过int最大值，返回int最大值 |
"-2147483649" |  -2147483648 | 小于int最小值，返回int最小值 |
"9223372036854775808" | "2147483647" | 超过了long的最大值，转换时应该try{}catch |
"-9223372036854775809" |-2147483648 | 小于long最小值，同上 |

```java
public class Solution {
    public int myAtoi(String str) {
        char []c = str.toCharArray();
        int start = 0;
        while(start<c.length){
            if(c[start] == ' ')
                start ++;
            else
                break;
        }
        int end = start;
        while(end<c.length){
            if((c[end]=='+' || c[end]=='-') && (end<c.length-1&&(c[end+1]>='0' && c[end+1]<='9')))
                end ++;
            if(c[end]>='0' && c[end]<='9')
                end++;
            else
                break;
        }
        String target = str.substring(start,end);
        if(target.length()==0)
            return 0;
        try{
            long result = Long.parseLong(target);
            if(result<Integer.MIN_VALUE)
                return Integer.MIN_VALUE;
            if(result>Integer.MAX_VALUE)
                return Integer.MAX_VALUE;
            return (int)result;
        }catch(Exception e){
            if(str.charAt(0)=='-')
                return Integer.MIN_VALUE;
            else
                return Integer.MAX_VALUE;
        }
    }
}
```

## 遇到的困难

>1. 对于字符串字符的操作，应该尽可能的转化成char数组操作，效率上高于直接操作字符串；
>2. 对于while的使用，以及判断是否存在连续的符号，或者正常的符号添加情况判断。

让我来看：

```java
while(end<c.length){
    if((c[end]=='+' || c[end]=='-') && (end<c.length-1&&(c[end+1]>='0' && c[end+1]<='9')))
        end ++;
    if(c[end]>='0' && c[end]<='9')
        end++;
    else
        break;
}
```
这里是困扰我一会的判断代码。