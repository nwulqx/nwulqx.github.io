---
title: 66. Plus One
date: 2017-04-24 16:29:33
tags:
- LeetCode-easy
- Array
---
Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.

<!--more-->


# 分析

其实，仔细看这道题，进位运算是这道题的考点。何时进位，如何进位，以及连续的进位应该怎么做？

**伪码**

```c
for(i<--digits[digits的长度-1];i>=0;i--){
    if(digits[i]<9){//这里很巧妙，小于9，则直接+1后return，如果能想到这里的话，基本上就很简单了
        digits[i]++;
        return digits;
    }else{
        digits[i] = 0;//这里其实只需要置0即可，因为这里最大的进位仅为1，所以不需要考虑大于1的进位
    }
}
newDigits数组 <-- 新数组[digits的长度+1]//到达了这一步仍没有返回，说明，每一位都是9，所以，出现了比原数组多了一位。
newDigits[0] <-- 1;
return newDigits;
```

**源码**

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/plus-one/
 * Runtime: 3 ms, faster than 54.04%
 * Memory Usage: 8.7 MB, less than 85.67%
 */
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function(grid) {
    const m = grid.length, n = grid[0].length;
    for(let i = 1; i < m; i++){
        grid[i][0] += grid[i-1][0];
    }
    for(let j = 1; j < n; j++){
        grid[0][j] += grid[0][j-1];
    }
    for(let i = 1; i < m; i++){
        for(let j = 1; j < n; j++){
            grid[i][j] += Math.min(grid[i-1][j], grid[i][j-1]);
        }
    }
    return grid[m-1][n-1];
};
```



**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/plus-one/
 * Runtime: 3 ms, faster than 54.04%
 * Memory Usage: 8.7 MB, less than 85.67%
 */
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int len = digits.size();
        int carry = 1;
        for(int i = len - 1; i >= 0; i--){
            digits[i] += carry;
            carry = digits[i] / 10;
            digits[i] %= 10;
        }
        if(carry > 0){
            digits.insert(digits.begin(), carry);
        }
        return digits;
    }
};
```



**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/plus-one/
 * Beats : 100%;
 */
public class PlusOne{
    public static int[] plusOne(int[] digits) {
        if(digits.length == 0)
            return digits;
        int i = digits.length-1;
        while(i>=0){
            if(digits[i]<9){
                digits[i]++;
                return digits;
            }else{
                digits[i] = 0;
                i--;
            }
        }
        int []newDigits = new int[digits.length+1];
        newDigits[0] = 1;
        return newDigits;
    }
}
```

**python实现**

```python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        i = len(digits) - 1;
        while i >= 0:
            if digits[i] < 9:
                digits[i] += 1
                return digits
            else:
                digits[i] = 0
                i -= 1
        digits.insert(0,1)
        return digits
```



## 思考

>2017年时，这道题其实对我来说很难。对于进位运算的操作和实践太少，思路也不够清晰。<br>
>
>2020年时，这道题对于我来说很简单了，没有难点，由于它的局限性，只是加1操作，对于加n操作的位运算，遇到了在进行分析。
>
>主要思路在于，对于位上是9的操作，只需要将该位置0，而对于位上小于9的操作，只需要该位加1，返回即可。这是加1运算的局限，不需要单独的进位变量，因为进位最大不会超过1。

# 总结

>进位运算其实很考察逻辑，需要注意的是进位。