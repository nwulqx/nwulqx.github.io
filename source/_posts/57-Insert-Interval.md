---
title: 57. Insert Interval
date: 2021-10-22 00:34:34
tags:
- Array
- interval(区间)
---

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` *after the insertion*.

 

**Example 1:**

```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```

<!--more-->

**Example 2:**

```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

**Example 3:**

```
Input: intervals = [], newInterval = [5,7]
Output: [[5,7]]
```

**Example 4:**

```
Input: intervals = [[1,5]], newInterval = [2,3]
Output: [[1,5]]
```

**Example 5:**

```
Input: intervals = [[1,5]], newInterval = [2,7]
Output: [[1,7]]
```

 

**Constraints:**

- `0 <= intervals.length <= 104`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 105`
- `intervals` is sorted by `starti` in **ascending** order.
- `newInterval.length == 2`
- `0 <= start <= end <= 105`

# Analysis

**c++**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/insert-interval/
 * Runtime: 16 ms, faster than 71.94%
 * Memory Usage: 17.2 MB, less than 40.97%
 */
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> res;
        int i = 0, n = intervals.size();
        while(i < n && intervals[i][1] < newInterval[0]){
            res.push_back(intervals[i]);
            i++;
        }
        while(i < n && intervals[i][0] <= newInterval[1]){
            newInterval[0] = min(intervals[i][0],newInterval[0]);
            newInterval[1] = max(intervals[i][1],newInterval[1]);
            i++;
        }
        res.push_back(newInterval);
        while(i < n){
            res.push_back(intervals[i]);
            i++;
        }
        return res;
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/insert-interval/
 * Runtime: 97 ms, faster than 48.86%
 * Memory Usage: 40.9 MB, less than 64.92%
 */
/**
 * @param {number[][]} intervals
 * @param {number[]} newInterval
 * @return {number[][]}
 */
var insert = function(intervals, newInterval) {
    const res = [], n = intervals.length;
    let index = 0;
    while(index < n && intervals[index][1] < newInterval[0]){
        res.push(intervals[index++]);
    }
    while(index < n && newInterval[1] >= intervals[index][0]){
        newInterval[0] = Math.min(newInterval[0],intervals[index][0]);
        newInterval[1] = Math.max(newInterval[1],intervals[index][1]);
        index++;
    }
    res.push(newInterval);
    while(index < n){
        res.push(intervals[index++]);
    }
    return res;
};
```

