---
title: Leetcode077-combinations
categories: leetcode
tags: [Backtracking]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-17 22:17:48
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

## Example
```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

## Solution
```java
class Solution {
    public void backtracking(List<List<Integer>> res, List<Integer> tmp, int k, int n, int start){
        if (tmp.size() == k){
            res.add(new ArrayList<Integer>(tmp));
            return;
        }
        for (int i = start;i <= n - (k-tmp.size()) + 1; i++){ //notice i<=n-(k-tmp.size())+1 speed up from 26ms downto 2ms
            tmp.add(i);
            backtracking(res, tmp, k, n, i+1);
            tmp.remove(tmp.size()-1);
        }
    }
    
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<>();
        if (k>n) return res;
        backtracking(res, new ArrayList<Integer>(), k, n, 1);
        return res;
    }
}
```

<hr />