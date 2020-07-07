---
title: Leetcode078-subsets
categories: leetcode
tags: [Backtracking, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-16 23:59:13
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a set of distinct integers, nums, return all possible subsets (the power set).

**Note**: The solution set must not contain duplicate subsets.

## Example
```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

## Solution
```java
class Solution {
    public void backtrack(List<List<Integer>> res, List<Integer> temp, int[] nums, int start){
        res.add(new ArrayList<Integer>(temp));
        for (int i = start; i < nums.length; i++){
            temp.add(nums[i]);
            backtrack(res, temp, nums, i + 1);
            temp.remove(temp.size()-1);
        }
    }
    
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(res, new ArrayList<Integer>(), nums, 0);      
        return res;
    }
}
```

<hr />