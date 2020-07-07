---
title: Leetcode453-minimumMovestoEqualArrayElements
categories: leetcode
tags: [Math, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-14 16:41:11
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty integer array of size n, find the minimum number of moves required to make all array elements equal, where a move is incrementing n - 1 elements by 1.

## Example
```
Input:
[1,2,3]

Output:
3

Explanation:
Only three moves are needed (remember each move increments two elements):

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```

## Solution
```java
class Solution {
    public int minMoves(int[] nums) {
        if (nums == null || nums.length == 0) return 0;        
//         sum + m(n-1) = x * n
//         x = minVal + m
//         => m = sum - n * minVal
        int sum = 0;
        int minVal = Integer.MAX_VALUE;
        for (int num: nums){
            sum += num;
            minVal = Math.min(minVal, num);
        }
        return sum - nums.length * minVal;        
    }
}
```

<hr />