---
title: 1.TwoSum
date: 2017-01-06 10:59:38
tags:
- LeetCode-easy
- 双指针+逼近法
---

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have ***exactly*** one solution.

**Example:**

	Given nums = [2, 7, 11, 15], target = 9,
	
	Because nums[0] + nums[1] = 2 + 7 = 9,
	return [0, 1].

<!--more-->

# 爆破法：
>通过遍历两次数组，找出所有两个数的组合，将结果与target比较，返回满足要求的索引。这种方法简单易懂，但是如果寻找三个数或者以上的多位相加，他的时间复杂度是指数增长的。

```java
import java.util.*;
/*
 * Standard Brute Forced method to solve;
 */
public class TwoSum{
	public static int[] twoSum(int[] nums, int target){
		for(int i = 0;i<nums.length;i++){
			for(int j = i+1;j<nums.length;j++){
				if(target-nums[i] == nums[j])
					return new int[] {i,j};
			}
		}
		throw new IllegalArgumentException("No Such Two Arguments");
	}
}
```

>上面这是一种标准的暴力破解方法，简单易懂，但是如果是找三个或者4个，这种多层的嵌套不利于实际操作和理解。应该借助下面这种封装的方式来避免多层（3层以上的）嵌套。

```java
import java.util.*;
/*
 * This method is a Brute Forced method.
 * time completicity is O(n2);
 * space complicity is O(1);
 * beats: 25%;
*/
public class TwoSum {
    public int[] twoSum(int[] nums, int target) {
    	int []ret = new int[2];
    	for(int i=0,j=i;i<nums.length;i++){
    			int tmp = target-nums[i];
    			if(ret[1]==0){
    				ret[0] = i; 
					ret[1] = this.find(nums,tmp,++j);
    			}else
    				break;
    	}
    	return ret;
    }
    public int find(int[] nums,int target,int lo){
    	int ret = 0;
    	for(int i=lo;i<nums.length;i++){
    		if(target<nums[i]) continue;
    		if(target == nums[i]){
    			ret = i;
    			break;
    		}
        }
        return ret;
    } 
}
```

# Hash法：
>HashMap的数据结构是树，使用HashMap，它的查询时的时间复杂度是O(n+logn)。
>

**Java实现**

```java
import java.util.*;
/*
 * app:leetcode lang:Java
 * https://leetcode.com/problems/two-sum/submissions/
 * Beats : 45%;
 * Time complicity is O(n);
 * Space complicity is O(n);
 */
public class TwoSum3{
	public static int[] twoSum(int[] nums, int target){
		Map<Integer,Integer> map = new HashMap();
		for(int i=0;i<nums.length;i++){
			map.put(nums[i],i);
		}
		for(int j=0;j<nums.length;j++){
			 // We don't need two same elements!
			if(map.containsKey(target-nums[j])&&(map.get(target-nums[j])!=j)){
				return new int[] {j,map.get(target-nums[j])};
			}
		}
		throw new IllegalArgumentException("No Such Two Arguments");
	}
}
```

**c++实现**

```c++
/*
 * app:leetcode lang:c++
 * https://leetcode.com/problems/two-sum/submissions/
 * Beats : 95.51%;
 */
#include <cstdio>
#include <vector>
#include <unordered_map>
using namespace std;
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		unordered_map<int, int> hash;
		vector<int> result;
		for (int i = 0; i < nums.size(); i++){
			int numToFind = target - nums[i];
			if (hash.find(numToFind) != hash.end()){
				result.push_back(hash[numToFind]);
				result.push_back(i);
				return result;
			}
			hash[nums[i]] = i;
		}
		return result;
	}
};
```

**python实现**

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        hash_dict = {}
        for i in range(len(nums)):
            numToFind = target - nums[i]
            if numToFind in hash_dict:
                return [hash_dict[numToFind],i]
            hash_dict[nums[i]] = i;

```



## 疑惑

>[{0,-2,0,0},0],对于这样的查询，HashMap中存放了相同的key的情况，是覆盖了前面
两个0的索引，所以答案是(0,3);


# 引申问题

>如果问题换成返回数组的值，而不是元素的索引，其实还有更好的办法。

## 逼近法
>1.将数组排序，使用快排或者归并排序，时间复杂度为O（nlogn）。<br>
2.使用两个索引，分别从头和尾部逼近，如果相加小于target，那么头部索引++；如果大于，则尾部索引--，直到找到。<br>
3.时间复杂度总共为O（nlogn+n）。<br>

>缺点：只能返回元素的值，由于排序打乱了索引。

```java
import java.util.*;
/*
 * This method is found the 2 nums sum is target ,but the return isn't the index!
 */
public class TwoSum4{
	//the return isn't index,it is a array of values
	public static int[] twoSum(int[] nums, int target){
		Arrays.sort(nums);
		int lo = 0;
		int hi = nums.length-1;
		while(lo<hi){
			if(nums[lo]+nums[hi]==target) return new int[]{nums[lo],nums[hi]};
			else if(nums[lo]+nums[hi] > target) hi--;
			else lo++;
		}
		throw new IllegalArgumentException("No Such Two Arguments");
	}
}
```

# 总结

>这道题有两个目的：

>1. 通过找两个数的和，接下来还有找三个数的四个数的，那么多层嵌套是非常反逻辑的，会把你带到逻辑漩涡里。所以，封装成找两个数的和，三个数的等这些`函数`后，那么问题被简化了。
>   2. 逼近法是一个很好的查找元素的思路，对于数组先排序，利用数组的有序性，通过`双索引+逼近法`。但是，缺点是排序打乱了索引，只能查找元素值。