---
title: 70. Climbing Stairs
date: 2017-04-25 17:39:18
tags:
- LeetCode-easy
- Optimize(优化)
- recursion(递归)
- DP(动态规划)
---
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
<!-- more -->

# Solution

## 分析

>这道题目，第一眼看过去，就是想到了递归解决。

**源码**
```java
public class ClimbingStairs{
	public int climbStairs(int n) {
		if(n == 1) return 1;
		if(n == 2) return 2;
		return climbStairs(n-1)+climbStairs(n-2);
	}
}
```
OK，AC不过。

	Time Limit Exceeded
	Last Input: 44

由于递归的占用内存很大，所以这里当输入44时，出现了超时。

**如何解决？**

>我记得，能用递归解决的问题，一定能用循环解决。那这道题换个思路，用循环。可以借用一下动态规划的方法。

**源码**

```java
public class ClimbingStairs{
	public int climbStairs(int n) {
		if(n == 1){
			return 1;
		}
		int arr[] = new int[n+1];
		arr[1] = 1;
		arr[2] = 2;
		for(int i=3;i<arr.length;i++){
			arr[i] = arr[i-1] + arr[i-2];
		}
		return arr[n];
	}
}
```

## 优化

至此，已经可以AC过了，但是。还是不够，因为它的空间复杂度是O(n)。仔细思考一下，其实它所需要的变量只要3个就够了，而不需要数组。

```java
public class Solution {
	public int climbStairs(int n) {
		if(n<=1){
			return 1;
		}
		if(n == 2){
			return 2;
		}
		int oneStepBefore = 2;
		int twoStepBefore = 1;
		int allWays = 0;
		/*
			1 2 3 5 8
			t o a
			  t o a
		*/
		for(int i=2;i<n;i++){
			allWays = oneStepBefore + twoStepBefore;
			twoStepBefore = oneStepBefore;
			oneStepBefore = allWays;
		}
		return allWays;
	}
}
```

# 总结

>能用递归解决的问题，一定要考虑他的开销，递归虽然很快捷，但是他的开销也很大，如果需要很深的递归，那么不妨考虑下使用动态规划。或者如果可能的情况下，一定要考虑下使用循环。以减少递归带来的问题。