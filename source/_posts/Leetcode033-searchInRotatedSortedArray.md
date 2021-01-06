---
title: Leetcode033-searchInRotatedSortedArray
categories: leetcode
tags: [Divide and Conquer, Amazon, Microsoft, Bloomberg, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-12 11:01:56
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

## Example
**Example 1:**
```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```
**Example 2:**
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```
## Solution
```java
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) return -1;

        int left = 0;
        int right = nums.length -1;
        while (left <=right){
            int mid = left + (right - left)/2;
            if (nums[mid] == target) return mid;
            
            if (nums[mid] <= nums[right]){
                if (target > nums[mid] && target <= nums[right]) left = mid + 1;
                else right = mid -1;
            }
            else{
                if (target >= nums[left] && target < nums[mid]) right = mid - 1;
                else left = mid + 1;
            }
        }
        return -1;
    }
}
```

<hr />