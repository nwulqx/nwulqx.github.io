---
title: 14. Longest Common Prefix
date: 2017-01-19 15:54:15
tags:
- LeetCode-easy
- Optimize(优化)
- 减法思维
---

Write a function to find the longest common prefix string amongst an array of strings.

<!--more-->

# Solution

## Brute Forced

>我的思路是做加法，每遍历一次字符串数组，就把最长前缀索引+1，直到某一个字符串不存在最长前缀为止。<br>
>这个太费时了，不做这种笨方法。<br>
>需要一个最长前缀索引，然后再遍历所有字符串，如果所有都存在相同的子字符串，则最长前缀索引+1，直到有字符串不包含这个最长前缀字符串，则返回。<br>
>那这个时间复杂度最坏情况下O(n*str.length)

## Optimized（优化）

>讲真的，我还真没什么想法，看了解答，恍然大悟。
>最好的思路是做减法：<br>
>
>1. 假设第一个字符串就是最长前缀，那么遍历字符串数组；
>2. 如果，后续的字符串长度小于最长前缀，那么这个最长前缀应该减1；
>3. 如果，字符串存在最小前缀，则应该继续检查字符串数组。这里有个很大的优势，如果，后续的字符串不符合最长前缀了，那么，不会影响到前面的判断，因为做的是减法（也就是b∈c的问题，最长前缀总是满足最短的原则）。
>4. 那么，如果不存在，则只需要对最长前缀字符串做减法即可。<br>
>5. 已经得到最长前缀索引，返回即可。

>这个题很巧妙的利用了减法的思想。<br>
>如果正着查找，那么需要知道每一个字串是否都存在于每一个字符串，如果存在，则在向后加一个字符，在比较。如果用这种减法的思路：先假设一个最长的前缀，如果不存在，应该减小这个最长前缀；如果存在，则应该对后面的字符串继续判断。好处很直观：
>
>1. 只需要遍历一次字符串数组；
>2. 时间复杂度O(n+strs[0].length)。


```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0 || strs[0].length()==0)
            return "";
        String  pre = strs[0];
        int hi = pre.length();
        int i = 1;
        while(i<strs.length && hi>0){
            if(strs[i].length()<hi)
                hi--;
            else if(strs[i].substring(0,hi).equals(pre.substring(0,hi)))
                i++;
            else
                hi--;
        }
        System.out.println(hi);
        return pre.substring(0,hi);
    }
}
```

**利用indexOf方法**

```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0 || strs[0].length()==0)
            return "";
        String  pre = strs[0];
        for(int i=1;i<strs.length;i++)
            while(strs[i].indexOf(pre.substring(0,pre.length()))!=0)
                pre = pre.substring(0,pre.length()-1);
        return pre;
    }
}
```

## Boundary Check

1. 字符串数组为0或者第一个字符串为0，应该返回空字符串。
2. 最长前缀为空或者遍历完字符串数组时结束。

# 总结

>利用了减法的思想来解决最长前缀问题。

P.S.

# <a href="https://war3cdota.github.io/2017/01/22/Longest-Common-Substring/">Longest Common Substring</a>