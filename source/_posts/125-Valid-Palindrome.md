---
title: 125. Valid Palindrome
date: 2017-06-19 10:38:47
tags:
- LeetCode-easy
- 双指针
---

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**For example,**

`"A man, a plan, a canal: Panama"` is a palindrome.<br>
`"race a car"` is not a palindrome.

**Note:**


Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

<!-- more -->

# Solution

## Solution 1

>使用正则表达式过滤。`[^a-zA-Z0-9]`，过滤非字符数字。

>这样做的效率比较低，因为正则表达式创建了一个新的空间，空间复杂度为O(n)。

```java
public class Solution {
    public boolean isPalindrome(String s) {
        s = s.replaceAll("[^a-zA-Z0-9]","");
        int i = 0,j=s.length()-1;
        while(i<=j){
            if(Character.toLowerCase(s.charAt(i)) != Character.toLowerCase(s.charAt(j)))
                return false;
            i++;
            j--;
        }
        return true;
    }
}
```

# Optimized

## Solution2

减少空间复杂度，直接判断，使用双指针和Character.isLetterOrDigit()方法，可以很方便的判断是否对称。

```java
public class Solution {
    public boolean isPalindrome(String s) {
        int low = 0;
        int high = s.length()-1;
        char arr[] = s.toLowerCase().toCharArray();
        while(low<=high){
            if(Character.isLetterOrDigit(arr[low]) && Character.isLetterOrDigit(arr[high])){
                if(arr[low] != arr[high]){
                    return false;
                }
                low++;
                high--;
            }else{
                if(!Character.isLetterOrDigit(arr[low])){
                    low++;
                }else if(!Character.isLetterOrDigit(arr[high])){
                    high--;
                }
            }
        }
        return true;
    }
}
```

# 总结
>这个题主要考察了对字符串中字符的操作，使用双指针方法是很不错的思路！