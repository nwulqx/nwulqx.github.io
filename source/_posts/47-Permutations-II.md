---
title: 47. Permutations II
date: 2021-10-21 21:07:22
tags:
- Array
- LeetCode-medium
- DFS(深度优先遍历)
- DFS去重
---

Given a collection of numbers, `nums`, that might contain duplicates, return *all possible unique permutations **in any order**.*

 

**Example 1:**

```
Input: nums = [1,1,2]
Output:
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

 <!-- more -->

**Example 2:**

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

 

**Constraints:**

- `1 <= nums.length <= 8`
- `-10 <= nums[i] <= 10`

# Analysis

**c++**

```c++
/*
 * app:leetcode lang: c++
 * https://leetcode.com/problems/permutations-ii/
 * Runtime: 13 ms, faster than 43.29%
 * Memory Usage: 9.7 MB, less than 42.14% 
 */
class Solution {
private:
    vector<int> nums;
    unordered_set<int> st;
    vector<int> path;
    vector<vector<int>> res;
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        this->nums = nums;
        dfs(0);
        return res;
    }
    void dfs(int level){
        if(level == nums.size()){
            res.push_back(path);
            return;
        }
        for(int i = 0; i < nums.size(); i++){
            if(st.find(i) != st.end()) continue;
            if(i > 0 && nums[i] == nums[i-1] && st.find(i-1) == st.end()) continue;
            st.insert(i);
            path.push_back(nums[i]);
            dfs(level+1);
            path.pop_back();
            st.erase(i);
        }
    }
};
```

**javascript**

```js
/*
 * app:leetcode lang: javascript
 * https://leetcode.com/problems/permutations-ii/
 * Runtime: 159 ms, faster than 37.61%
 * Memory Usage: 42 MB, less than 84.62%
 */
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permuteUnique = function(nums) {
    const res = [];
    const path = [];
    const st = new Set();
    nums.sort((a,b) => a-b);
    function dfs(level){
        if(level === nums.length){
            res.push([...path]);
            return;
        }
        for(let i = 0;i < nums.length; i++){
            if(st.has(i)) continue;
            if(i > 0 && nums[i] === nums[i-1] && !st.has(i-1)) continue;
            st.add(i);
            path.push(nums[i]);
            dfs(level+1);
            path.pop();
            st.delete(i);
        }
    }
    dfs(0);
    return res;
};
```

