---
title: 119. Pascal's Triangle II
date: 2017-06-01 17:28:36
tags:
- LeetCode-easy
- Pascal's Triangle(杨辉三角形)
- Array
---
Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return `[1,3,3,1]`.

**Note:**

Could you optimize your algorithm to use only O(k) extra space?

<!-- more -->
# 分析

## Solution1

**通过上层来计算当前行**，这个解法就是118. Pascal's Triangle的解法。

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/pascals-triangle-ii
 * Runtime: 64 ms, faster than 96.55%
 * Memory Usage: 38.7 MB, less than 56.63%
 */
/**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(rowIndex) {
    const level = [1];
    for(let i = 1; i <= rowIndex; i++){
        level.push(1);
        for(let j = level.length-2; j > 0; j--){
            level[j] += level[j-1];
        }
    }
    return level;
};
```

**c++**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/pascals-triangle-ii
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 6.2 MB, less than 99.24%
 */
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> level(1,1);
        for(int i = 1; i <= rowIndex; i++){
            level.push_back(1);
            for(int j = level.size()-2; j > 0; j--){
                level[j] += level[j-1];
            }
        }
        return level;
    }
};
```



**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/pascals-triangle-ii
 * Beats : 100%;
 */
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

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/pascals-triangle-ii
 * Beats : 100%;
 */
class Solution {
public:
    vector<int> getRow(int rowIndex) {
		vector<int> result;
		for (int i = 0; i <= rowIndex; i++){
			result.push_back(1);
			for (int j = result.size() - 2; j > 0; j--){
				result[j] += result[j - 1];
			}
		}
		return result;
    }
};
```

**python实现**

```python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        result = []
        for i in range(0,rowIndex+1):
            result.append(1)
            for j in range(len(result)-2,0,-1):
                result[j] = result[j]+result[j-1]
        return result
```



## Solution2

>其实这个计算是有公式的。

## <a href="https://en.wikipedia.org/wiki/Pascal%27s_triangle#Calculating_a_row_or_diagonal_by_itself">Calculating a row or diagonal by itself</a>

>当前行的值可以通过，改之所在行和索引来计算。
>
>k表示第k行，i表示该行的第i个元素。他们之间的关系有如下的公式：
>
>$ C[k,i] = C[k,i-1] \times (k-i+1)\div i $
>
>例如：k=5时
>
>$ C[5,0] = 1$
>
>$ C[5,1] = C[5,0] \times (5-1+1) \div 1 = 5$
>
>$ C[5,2] = C[5,1] \times (5-2+1) \div 2 = 10$
>
>......

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/pascals-triangle-ii
 * Beats : 100%;
 */
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

对于这种Pascal's Triangle（杨辉三角）类型的题目，如果想计算它，我们知道有两种方法：

1. 直接在一行首或尾加1，然后计算下一行。例如：1,2,1 ---> 1,2,1,1 ---> 1,3,3,1
2. 根据$ C[k,i] = C[k,i-1] \times (k-i+1)\div i $，可以直接计算当前行，所根据的只是当前行号和当前行的元素索引，而不需要知道上一行的内容。