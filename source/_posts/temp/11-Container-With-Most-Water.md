---
title: 11. Container With Most Water
date: 2018-02-04 14:07:37
tags:
- LeetCode-medium
- 双指针+逼近法
- Array
---

Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and *n* is at least 2.

![Alt text](/images/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

 

**Example:**

```java
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

<!--more-->

# 分析

这道题目一开始，我定位在动态规划问题，在实现的时候遇到了不能解决的逻辑上的问题，只好参考了别人的解法。

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

**c++实现**

```c++
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