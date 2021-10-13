---
title: 134. Gas Station
date: 2021-09-20 18:56:03
tags:
- Array
- LeetCode-medium
- Optimize(优化)
---

There are `n` gas stations along a circular route, where the amount of gas at the `ith` station is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `ith` station to its next `(i + 1)th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return *the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return* `-1`. If there exists a solution, it is **guaranteed** to be **unique**

  <!-- more -->

**Example 1:**

```
Input: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
Output: 3
Explanation:
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.
```

**Example 2:**

```
Input: gas = [2,3,4], cost = [3,4,3]
Output: -1
Explanation:
You can't start at station 0 or 1, as there is not enough gas to travel to the next station.
Let's start at station 2 and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 0. Your tank = 4 - 3 + 2 = 3
Travel to station 1. Your tank = 3 - 3 + 3 = 3
You cannot travel back to station 2, as it requires 4 unit of gas but you only have 3.
Therefore, you can't travel around the circuit once no matter where you start.
```

 

**Constraints:**

- `gas.length == n`
- `cost.length == n`
- `1 <= n <= 104`
- `0 <= gas[i], cost[i] <= 104`

# 分析

参考；https://www.liuchuo.net/archives/1224

这道题目其实挺难的，主要在于需要先判断是否能走完一圈，这个并不一定需要先找到开始位置才可以判断。其实循环全部 `gas[i]-cost[i]`就可得到总和来判断。

- 接着去找一个结点，该节点必须满足当前及以后的`gas[i]-cost[i]`大于0，就是需要的了

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/gas-station/
 */
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int total = 0, tank = 0, start = 0;
        for(int i = 0; i < gas.size(); i++){
            total += gas[i] - cost[i];
            if(tank >= 0){
                tank += gas[i] - cost[i];
            }else {
                start = i;
                tank = gas[i] - cost[i];
            }
        }
        return total >= 0? start:-1;
    }
};
```

```js
/**
 * @param {number[]} gas
 * @param {number[]} cost
 * @return {number}
 */
var canCompleteCircuit = function(gas, cost) {
    let total = 0, tank = 0, start = 0;
    for(let i = 0; i < gas.length; i++){
        total += gas[i] - cost[i];
        if(tank >= 0){
            tank += gas[i] - cost[i];
        }else{
            start = i;
            tank = gas[i] - cost[i];
        }
    }
    return total>=0?start:-1;
};
```

