---
title: 118. Pascal's Triangle
date: 2017-05-31 09:40:13
tags:
- LeetCode-easy
- Pascal's Triangle(杨辉三角形)
- Array
---

Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,

Return

```java
	[
	     [1],
	    [1,1],
	   [1,2,1],
	  [1,3,3,1],
	 [1,4,6,4,1]
	]
```

<!-- more -->
# 分析

## 暴力法

>暴力法，不需要知道规律，只要根据输入，得出输出即可。

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/pascals-triangle
 * Beats : 90%;
 */
public class PascalsTriangle{
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if(numRows==0) return result;
        List<Integer> list = new ArrayList<Integer>();
        list.add(1);
        result.add(list);
        while(numRows>1){
            list = generate(list);
            result.add(list);
            numRows--;
        }
        return result;
    }
    public List<Integer> generate(List<Integer> list){
        List<Integer> result = new ArrayList<Integer>();
        for(int i=0;i<list.size();i++){
            if(i>0){
                result.add(list.get(i-1)+list.get(i));
            }else{
                result.add(list.get(i));
            }
        }
        result.add(1);
        return result;
    }
}
```

## 优化

>找规律，发现，每次比上层多一个元素。规律也很容易发现，需要用循环解决。


```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/pascals-triangle
 * Beats : 100%;
 */
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        for(int i = 0 ;i < numRows; i++){
            list.add(1);
            for(int j = list.size()-2;j > 0;j--){
                list.set(j,list.get(j)+list.get(j-1));
            }
            /*
             * 这里为什么要new呢？因为Java和python都是将引用直接加进去的，所以结果是最后一次循环的结果的多次，因为他们并没有被复制，而是一个引用的多次
             * 比如：[[1,4,6,4,1],[1,4,6,4,1],[1,4,6,4,1],[1,4,6,4,1],[1,4,6,4,1]]
             * 不是我们希望的结果
             */
            result.add(new ArrayList<Integer>(list));
        }
        return result;
    }
}
```

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/pascals-triangle
 * Beats : 100%;
 */
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
		vector<vector<int>> result;
		vector<int> every;
		for (int i = 0; i < numRows; i++){
			every.push_back(1);
			for (int j = every.size() - 2; j >= 1; j--){
				every[j] += every[j - 1];
			}
            /*
             * 这里是很值得分析下的：可以看出vector是将引用的复制push进去的，而不是引用本身。
             * 这个是与Java和python很有区别的。
             */
			result.push_back(every);
		}
		return result;
    }
};
```

**python实现**

```python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        res = []
        list = []
        for i in range(0,numRows):
            list.append(1)
            for i in range(len(list)-2,0,-1):
                list[i] = list[i]+list[i-1]
            """注意这里和Java的原因一样"""
            tmp = list[:]
            res.append(tmp)
        return res
```



**注意：**

>这里思路，很简单，实际操作可以多次尝试得出正确循环体，包括在list的前面加1，还是在最后加1都是正确的。

>Java中`result.add(new ArrayList<Integer>(list));`和python中`res.append(tmp)`与
>
>c++中`result.push_back(every);`相区别，c++对引用进行了复制后再添加，而Java和python则直接将索引添加，这导致了不同的结果。`需要特别注意！`

# 总结

>1. 寻找规律。
> 2. 注意引用的复制问题。