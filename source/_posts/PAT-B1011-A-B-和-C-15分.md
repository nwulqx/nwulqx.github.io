---
title: PAT B1011 A+B 和 C (15分)
date: 2019-12-05 12:58:08
tags:
- PAT
- PAT-Basic
---

给定区间 $[−2^{31},2^{31}]$ 内的 3 个整数 A、B 和 C，请判断 A+B 是否大于 C。

<!--more-->

**输入格式：**

输入第 1 行给出正整数 T (≤10)，是测试用例的个数。随后给出 T 组测试用例，每组占一行，顺序给出 A、B 和 C。整数间以空格分隔。

**输出格式：**

对每组测试用例，在一行中输出 `Case #X: true` 如果 A+B>C，否则输出 `Case #X: false`，其中 `X `是测试用例的编号（从 1 开始）。

**输入样例：**

	4
	1 2 3
	2 3 4
	2147483647 0 2147483646
	0 -2147483648 -2147483647



**输出样例：**

	Case #1: false
	Case #2: true
	Case #3: true
	Case #4: false

## 分析

1. 因为在给定区间 $[-2^{31},2^{31}]$判断，该区间右端点在int范围已经溢出，且$−2^{31}+(−2^{31}) = −2^{32}$也在`int`范围是溢出的，说明加数，和均会溢出。所以不能使用`int`类型存储输入数据，需要用`long long`类型来保证计算不会溢出。

```c++
/*
 * app=PAT-Basic lang=c++
 * https://pintia.cn/problem-sets/994805260223102976/problems/994805312417021952
 */
#include <cstdio>
int main()
{
    int T;
    long long A, B, C,sum;
    scanf("%d",&T);
    for (int i = 0; i < T;i++){
        scanf("%lld%lld%lld",&A,&B,&C);
        sum = A + B;
        if (sum > C){
            printf("Case #%d: true\n",i + 1);
        }
        else{
            printf("Case #%d: false\n", i + 1);
        }
    }
    return 0;
}
```