---
title: Leetcode162-Find Peek Element
categories: leetcode
tags: [Array, Binary Search, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-05 23:14:29
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

A peak element is an element that is strictly greater than its neighbors.

Given an integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.

You may imagine that nums[-1] = nums[n] = -∞.

## Example

**Example 1:**
```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```
**Example 2:**
```
Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.
``` 

**Constraints:**

* 1 <= nums.length <= 1000
* -231 <= nums[i] <= 231 - 1
* nums[i] != nums[i + 1] for all valid i.

## Solution

* Time Complexity: $$O(log^N)$$
* Space Complexity: $$O(1)$$

```java
    public int findPeakElement(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        while(left < right){
            int mid1 = (left + right)/2;
            int mid2 = mid1 + 1;
            if (nums[mid1] < nums[mid2])
                left = mid2;
            else
                right = mid1;
        }
        return left;
    }
```

<hr />