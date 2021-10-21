---
title: 56. Merge Intervals
date: 2021-10-22 00:34:17
tags:
- Array
- interval(区间)
---

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return *an array of the non-overlapping intervals that cover all the intervals in the input*.

 

**Example 1:**

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

<!--more-->

**Example 2:**

```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

 

**Constraints:**

- `1 <= intervals.length <= 104`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 104`

# Analysis

**c++**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/merge-intervals/
 * Runtime: 128 ms, faster than 5.40%
 * Memory Usage: 28.5 MB, less than 5.19%
 */
class Solution {
public:
    static bool cmp(vector<int> a, vector<int> b){
        return a[0] < b[0];
    }
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<vector<int>> res;
        sort(intervals.begin(), intervals.end(), cmp);
        res.push_back(intervals[0]);
        for(int i = 1; i < intervals.size(); i++){
            if(intervals[i][0] > res.back()[1]){
                res.push_back(intervals[i]);
            }else{
                res.back()[1] = max(intervals[i][1],res.back()[1]);
            }
        }
        return res;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/merge-intervals/
 * Runtime: 80 ms, faster than 91.79%
 * Memory Usage: 40.8 MB, less than 53.60%
 */
/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */
var merge = function(intervals) {
    const res = [];
    intervals.sort((a,b) => a[0]-b[0]);
    res.push(intervals[0]);
    for(let i = 1; i < intervals.length; i++){
        if(intervals[i][0] > res[res.length-1][1]){
            res.push(intervals[i]);
        }else{
            res[res.length-1][1] = Math.max(res[res.length-1][1], intervals[i][1]);
        }
    }
    return res;
};
```

