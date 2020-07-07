---
title: Leetcode045-jumpGameII
categories: leetcode
tags: [Array, Greedy, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-06 15:18:49
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

## Example
```
Input: [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2.
    Jump 1 step from index 0 to 1, then 3 steps to the last index.
```
**Note:**

You can assume that you can always reach the last index.

## Solution
```java
class Solution {
    public int jump(int[] nums) {
        if (nums == null || nums.length == 0) return 0;

        int res = 0;
        int cur = 0;
        int last = 0;
        for (int i = 0; i < nums.length - 1; i++){
            cur = Math.max(cur, i+nums[i]);
            if (i == last){
                last = cur;
                res++;
            }
        }
        return res;
    }
}
```

<hr />