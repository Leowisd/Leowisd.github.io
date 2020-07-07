---
title: Leetcode035-searchInsertPosition
categories: leetcode
tags: [Array, Binary Search]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-11-04 14:27:01
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

## Example
**Example 1:**
```
Input: [1,3,5,6], 5
Output: 2
```
**Example 2:**
```
Input: [1,3,5,6], 2
Output: 1
```
**Example 3:**
```
Input: [1,3,5,6], 7
Output: 4
```
**Example 4:**
```
Input: [1,3,5,6], 0
Output: 0
```
## Solution
```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        if (nums == null || nums.length == 0) return 0;
        
        // O(logn) Method, Binary Search   
        if (target > nums[nums.length - 1]) return nums.length;
        int left = 0;
        int right = nums.length - 1;
        while(left < right){
            int mid = left + (right - left)/2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] < target) left = mid + 1;
            else right = mid;        
        }
        return left;
        
        // O(n) Method
        // for (int i = 0; i < nums.length; i++){
        //     if (target <= nums[i]) return i;
        // }
        // return nums.length;
    }
}
```

<hr />