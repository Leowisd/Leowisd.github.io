---
title: Leetcode034-findFirstAndLastPositionOfElementInSortedArray
categories: leetcode
tags: [Array, Binary Search, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-16 21:21:46
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

## Example
**Example 1:**
```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```
**Example 2:**
```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

## Solution
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if (nums == null || nums.length == 0) return new int[]{-1, -1};
        int smallest = findSmall(nums, target);
        int highest = findHigh(nums, target);
        int[] res = new int[]{smallest, highest};
        return res;
    }
    private int findSmall(int[] nums, int target){
        int left = 0;
        int right = nums.length - 1;
        int res = -1;
        while(left <= right){
            int mid = (left + right) / 2;
            if (nums[mid] == target) res = mid;
            if (nums[mid] >= target)
                right = mid - 1;
            else left = mid + 1;
        }
        return res;
    }
    private int findHigh(int[] nums, int target){
        int left = 0;
        int right = nums.length - 1;
        int res = -1;
        while(left <= right){
            int mid = (left + right) / 2;
            if (nums[mid] == target) res = mid;
            if (nums[mid] <= target)
                left = mid + 1;
            else right = mid - 1;
        }
        return res;
    }
}
```

<hr />