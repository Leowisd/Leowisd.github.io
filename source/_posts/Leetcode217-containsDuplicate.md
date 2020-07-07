---
title: Leetcode217-containsDuplicate
categories: leetcode
tags: [Hash Table, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-14 11:47:51
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

## Example
**Example 1:**
```
Input: [1,2,3,1]
Output: true
```
**Example 2:**
```
Input: [1,2,3,4]
Output: false
```
**Example 3:**
```
Input: [1,1,1,3,3,4,3,2,4,2]
Output: true
```

## Solution
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int num: nums){
            if (set.contains(num)) return true;
            set.add(num);
        }
        return false;
    }
}
```

<hr />