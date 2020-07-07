---
title: Leetcode040-combinationSumII
categories: leetcode
tags: [Backtracking]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-17 23:45:39
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

Each number in candidates may only be used once in the combination.

**Note:**

* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.

## Example
**Example** 1:
```
Input: candidates = [10,1,2,7,6,1,5], target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```
**Example** 2:
```
Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]
```
## Solution
```java
class Solution {
    public void backtracking(List<List<Integer>> res, List<Integer> tmp, int[] nums, int target, int start, int sum){
        if (sum == target){
            res.add(new ArrayList<>(tmp));
            return;
        } 
        for (int i = start; i < nums.length; i++){
            if (i > start && nums[i] == nums[i-1]) continue;
            tmp.add(nums[i]);
            if (sum + nums[i] <= target) backtracking(res, tmp, nums, target, i + 1, sum + nums[i]);
            else {
                tmp.remove(tmp.size()-1);
                return;
            }
            tmp.remove(tmp.size() - 1);
        }
    }
    
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        if (candidates == null) return res;
        Arrays.sort(candidates);
        backtracking(res, new ArrayList<Integer>(), candidates, target, 0, 0);
        return res;
    }
}
```

<hr />