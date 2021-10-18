---
title: 11. Container With Most Water
date: 2018-02-04 14:07:37
tags:
- LeetCode-medium
- 双指针+逼近法
- Array
- greedy(贪心)
---

Given `n` non-negative integers `a1, a2, ..., an` , where each represents a point at coordinate `(i, ai)`. `n` vertical lines are drawn such that the two endpoints of the line `i` is at `(i, ai)` and `(i, 0)`. Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

**Notice** that you may not slant the container.

 

**Example 1:**

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

<!--more-->

**Example 2:**

```
Input: height = [1,1]
Output: 1
```

**Example 3:**

```
Input: height = [4,3,2,1,4]
Output: 16
```

**Example 4:**

```
Input: height = [1,2,1]
Output: 2
```

 

**Constraints:**

- `n == height.length`
- `2 <= n <= 105`
- `0 <= height[i] <= 104`

# 分析

这道题目一开始，我定位在~~动态规划~~问题，其实是**贪心问题**，在实现的时候遇到了不能解决的逻辑上的问题，只好参考了别人的解法。

发现其实这道题目是二分法问题，具体实现可以用双指针实现。

## 证明

```java
if(height[low] < height[high]) {
    low++;
}else {
    high--;
}
```

这段逻辑的证明：当`height[low] < height[high]`时，如果`high--`，那么`Math.min(height[low], height[high])*(high-low);`**一定小于原来的面积**，这个可以根据图来分析。逻辑上，开始当以`height[low]`作为高，此时如果`high--`，且`height[low]<height[high]`时，那么仍以`height[low]`作为高的矩形一定更小，因为长一定变短（索引减小了）；而另一种情况当`height[high]<height[low]`时，不仅长变短了，而且高也变短了，高为`height[high]`了，面积一定小于原面积。所以就没必要使`high--`了，因为一定是小于原面积的，此时，需要`low++`来查找下一个面积了。

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/container-with-most-water/
 * Runtime: 166 ms, faster than 13.19%
 * Memory Usage: 59 MB, less than 39.38%
 */
class Solution {
public:
    int maxArea(vector<int>& height) {
		int low = 0, high = height.size() - 1;
		int area = 0;
		while (low < high){
			area = max(area,min(height[low],height[high])*(high - low));
			if (height[low] < height[high]){
				low++;
			}
			else{
				high--;
			}
		}
			return area;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang:javascript
 * https://leetcode.com/problems/container-with-most-water/
 * Runtime: 96 ms, faster than 52.70% 
 * Memory Usage: 48.1 MB, less than 28.98%
 */
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
    let low = 0, high = height.length - 1, res = 0;
    while(low <= high){
        const sum = (high-low) * Math.min(height[low],height[high]);
        res = Math.max(sum,res);
        if(height[low] < height[high]) low++;
        else high--;
    }
    return res;
};
```

**Java实现**

```java
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/container-with-most-water
 * Beats : 95.02%
 * Time complicity is O(logn);
 * Space complicity is O(1);
 */
class Solution {
    public int maxArea(int[] height) {
        int low = 0,high = height.length - 1;
        int area = 0;
        while(low < high) {
            int sum = Math.min(height[low], height[high])*(high-low);
            area = sum >area?sum:area;
            if(height[low] < height[high]) {
                low++;
            }else {
                high--;
            }
        }
        return area;
    }
}
```

**python实现**

```python
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        low = 0
        high = len(height) - 1
        area = 0
        while low < high:
            area = max(area,min(height[low],height[high])*(high-low))
            if height[low] < height[high]:
                low += 1
            else:
                high -= 1
        return area
```

# 总结

1. 如何定位，这道题，难在定位上，如何分析题目类型很重要，一开始我定位在了动态规划上，结果解不出来，最后使用双指针解决了。
2. 本题难点，在于双指针的条件判断上。