---
title: Leetcode229-majorityElementII
categories: leetcode
tags: [Array, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-10 18:58:33
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

Note: The algorithm should run in linear time and in O(1) space.

## Example
**Example 1:**
```
Input: [3,2,3]
Output: [3]
```
**Example 2:**
```
Input: [1,1,1,3,3,2,2,2]
Output: [1,2]
```

## Solution
```java
// Boyer-Moore Majority Algorithm
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        if (nums == null || nums.length == 0) return new ArrayList<>();
        int candidate1 = nums[0], candidate2 = nums[0];
        int count1 = 0, count2 = 0;
        for (int num: nums){
            if (candidate1 == num)
                count1++;
            else if (candidate2 == num)
                count2++;
            else if (count1 == 0){
                candidate1 = num;
                count1++;
            }
            else if (count2 == 0){
                candidate2 = num;
                count2++;
            }
            else{
                count1--;
                count2--;
            }
        }
        
        List<Integer> res = new ArrayList<>();
        count1 = 0;
        count2 = 0;
        for (int num: nums){
            if (candidate1 == num) count1++;
            if (candidate2 == num) count2++;
        }
        if (count1 > nums.length / 3)
            res.add(candidate1);
        if (candidate1 != candidate2 && count2 > nums.length / 3)
            res.add(candidate2);
        return res;
    }
}
```

<hr />