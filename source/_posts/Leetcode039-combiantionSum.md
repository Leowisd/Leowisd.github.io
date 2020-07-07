---
title: Leetcode039-combiantionSum
categories: leetcode
tags: [Backtracking, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-17 23:16:00
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times.

**Note:**

* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.

## Example

**Example** 1:
```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```
**Example** 2:
```
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```
## Solution
```java
class Solution {
    public void backtracking(List<List<Integer>> res, List<Integer> tmp, int[] nums, int target, int start, int sum){
        if (sum == target){
            res.add(new ArrayList<Integer>(tmp));
            return;
        }
        for (int i = start; i < nums.length; i++){
            tmp.add(nums[i]);
            if (sum + nums[i] <= target) backtracking(res, tmp, nums, target, i, sum + nums[i]);
            else{
                tmp.remove(tmp.size()-1);
                return;
            }
            tmp.remove(tmp.size()-1);            
        }
    }
    
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        if (candidates == null) return res;
        Arrays.sort(candidates);
        backtracking(res, new ArrayList<Integer>(), candidates, target, 0, 0);
        return res;
    }
}
```

<hr />