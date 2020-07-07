---
title: Leetcode047-permutationsII
categories: leetcode
tags: [Backtracking, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-16 21:28:38
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

## Example
```
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

## Solution
```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length == 0) return res;
        Arrays.sort(nums);
        boolean[] visited = new boolean[nums.length];
        helper(nums, res, new ArrayList<>(), visited);
        return res;
    }
    
    private void helper(int[] nums, List<List<Integer>> res, List<Integer> cur, boolean[] visited){
        if (cur.size() == nums.length){
            res.add(new ArrayList<>(cur));
            return;
        }
        
        for (int i = 0; i < nums.length; i++){
            if (visited[i]) continue;
            if (i > 0 && nums[i] == nums[i - 1] && !visited[i - 1]) continue;
            cur.add(nums[i]);
            visited[i] = true;
            helper(nums, res, cur, visited);
            visited[i] = false;
            cur.remove(cur.size() - 1);
        }
    }
}
```

<hr />