---
title: 150. Evaluate Reverse Polish Notation
date: 2021-09-20 19:11:53
tags:
- Array
- LeetCode-medium
- 逆波兰式(Reverse Polish Notation)
---

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are `+`, `-`, `*`, and `/`. Each operand may be an integer or another expression.

**Note** that division between two integers should truncate toward zero.

It is guaranteed that the given RPN expression is always valid. That means the expression would always evaluate to a result, and there will not be any division by zero operation.

 <!-- more -->

**Example 1:**

```
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

**Example 2:**

```
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

**Example 3:**

```
Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

 

**Constraints:**

- `1 <= tokens.length <= 104`
- `tokens[i]` is either an operator: `"+"`, `"-"`, `"*"`, or `"/"`, or an integer in the range `[-200, 200]`.

# 分析

这个问题本身算法不难，关键在于使用JavaScript发现了一些小问题，而其中涉及了js数值的保存，由于c++,java等语言使用补码处理整数，所以在int取整的处理是自然的向0取整。而在JS中，浮点数的负数取整则是向下取整，这个逻辑导致了在JS中使用Math.floor()导致一个结点不通过了。所以这里使用Math.trunc()直接省去小数点数字~

```js
/**
 * @param {string[]} tokens
 * @return {number}
 */
var evalRPN = function(tokens) {
    const stack = [];
    for(let a of tokens){
        if(a === '+') {
            const x = stack.pop();
            const y = stack.pop();
            stack.push(x+y);
        }
        else if(a === '*') {
            const x = stack.pop();
            const y = stack.pop();
            stack.push(x*y);
        }
        else if(a === '-') {
            const x = stack.pop();
            const y = stack.pop();
            stack.push(y-x);
        }
        else if(a === '/') {
            const x = stack.pop();
            const y = stack.pop();
            stack.push(Math.trunc(y/x));
        }
        else{
            stack.push(Number(a));
        }
    }
    return stack.pop();
};
```

```c++
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;
        for(string s : tokens){
            if(s == "+"){
                int a = st.top();
                st.pop();
                int b = st.top();
                st.pop();
                st.push(a+b);
            }
            else if(s == "-"){
                int a = st.top();
                st.pop();
                int b = st.top();
                st.pop();
                st.push(b-a);
            }
            else if(s == "*"){
                int a = st.top();
                st.pop();
                int b = st.top();
                st.pop();
                st.push(a*b);
            }
            else if(s == "/"){
                int a = st.top();
                st.pop();
                int b = st.top();
                st.pop();
                st.push(b/a);
            }
            else{
                int c = stoi(s);
                st.push(c);
            }
        }
        return st.top();
    }
};
```

