---
title: Leetcode046-permutations
categories: leetcode
tags: [Backtracking, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 21:46:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a collection of distinct integers, return all possible permutations.

## Example
```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

## Solution
```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length == 0) return res;
        
        boolean[] visited = new boolean[nums.length];
        helper(nums, res, new ArrayList<Integer>(), visited);
        
        return res;
    }
    
    private void helper(int[] nums, List<List<Integer>> res, List<Integer> cur, boolean[] visited){
        if (cur.size() == nums.length){
            res.add(new ArrayList<Integer>(cur));
            return;
        }
        
        for (int i = 0; i < nums.length; i++){
            if (!visited[i]){
                visited[i] = true;
                cur.add(nums[i]);
                helper(nums, res, cur, visited);
                cur.remove(cur.size() - 1);
                visited[i] = false;
            }
        }
    }
}
```

<hr />