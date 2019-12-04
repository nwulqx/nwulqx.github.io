---
title: 119. Pascal's Triangle II
date: 2017-06-01 17:28:36
tags:
- LeetCode-easy
- Pascal's Triangle(杨辉三角形)
---
Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return `[1,3,3,1]`.

**Note:**

Could you optimize your algorithm to use only O(k) extra space?

<!-- more -->
# Solution

## Solution1

**通过上层来计算当前行**

```java
public class PascalsTriangleII4{
    public List<Integer> getRow(int rowIndex) {
        List<Integer> list = new ArrayList<Integer>();
        for(int i=0;i<rowIndex;i++){
            list.add(0,1);
            for(int j=1;j<list.size()-1;j++){
                list.set(j,list.get(j)+list.get(j+1));
            }
        }
        return list;
    }
}
```

## Solution2

>其实这个计算是有公式的。

## <a href="https://en.wikipedia.org/wiki/Pascal%27s_triangle#Calculating_a_row_or_diagonal_by_itself">Calculating a row or diagonal by itself</a>

>当前行的值可以通过，改之所在行和索引来计算。

C[k,i] = C[k,i-1]*(k-i+1)/i

k为第几行，i为该行第几个数。

```java
public class PascalsTriangleII{
    public List<Integer> getRow(int rowIndex) {
        Integer []rowarray = new Integer[rowIndex+1];
        rowarray[0] = 1;
        for(int i=1;i<rowarray.length;i++){
            rowarray[i] = (int)((long)rowarray[i-1]*(rowIndex+1-i)/(i));
        }
        return Arrays.asList(rowarray);
    }
}
```

# 总结

>这个题目没什么新意，<a href="https://war3cdota.github.io/2017/05/31/118-Pascal-s-Triangle/">118. Pascal's Triangle</a>，最后的公式计算需要记一下。