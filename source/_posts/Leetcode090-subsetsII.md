---
title: Leetcode090-subsetsII
categories: leetcode
tags: [Backtracking]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-17 00:07:49
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).

**Note**: The solution set must not contain duplicate subsets.

## Example
```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
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
            if (i > start && nums[i] == nums[i-1]) continue;
            temp.add(nums[i]);
            backtrack(res, temp, nums, i+1);
            temp.remove(temp.size()-1);
        }
    }
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        backtrack(res, new ArrayList<Integer>(), nums, 0);
        return res;
    }
}
```

<hr />