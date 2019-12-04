---
title: 118. Pascal's Triangle
date: 2017-05-31 09:40:13
tags:
- LeetCode-easy
- Pascal's Triangle(杨辉三角形)
---

Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,

Return

		[
		     [1],
		    [1,1],
		   [1,2,1],
		  [1,3,3,1],
		 [1,4,6,4,1]
		]

<!-- more -->
# Solution

## Solution1

>笨方法，不需要知道规律，只要根据输入，得出输出即可。

```java
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

## Solution2

>找规律，发现，每次比上层多一个元素。规律也很容易发现，需要循环解决。


```java
public class PascalsTriangle{
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        for(int i=0;i<numRows;i++){
            list.add(0,1);
            for(int j=1;j<list.size()-1;j++){
                list.set(j,list.get(j+1) + list.get(j));
            }
            result.add(new ArrayList<Integer>(list));
        }
        return result;
    }
}
```

**注意：**

>这里思路，很简单，但是其实是根据很多次尝试得出的，包括在list的前面加1，而不是最后加1，因为如果在后面加一，会导致每次获取当前值变得复杂。

>`result.add(new ArrayList<Integer>(list));`这行犯了错误，是指针的问题，我觉得需要特别注意！

# 总结

>这个题目其实找到规律就很简单了：
> 1. 规律，正确的写法。
> 2. 指针的注意。