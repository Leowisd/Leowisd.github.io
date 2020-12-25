---
title: Leetcode493-reversePairs
categories: leetcode
tags: [Merge Sort, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-12-24 12:21:21
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array nums, we call (i, j) an important reverse pair if i < j and nums[i] > 2*nums[j].

You need to return the number of important reverse pairs in the given array.

## Example
**Example1:**
```
Input: [1,3,2,3,1]
Output: 2
```
**Example2:**
```
Input: [2,4,3,5,1]
Output: 3
```

## Solution

* Time Complexity: $$O(Nlog^N)$$
* Space Complexity: $$O(N)$$

```java
class Solution {
    public int reversePairs(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        return mergeSort(nums, 0, nums.length - 1);
    }
    
    private int mergeSort(int[] nums, int left, int right){
        if (left >= right) return 0;
        int mid = left + (right - left) / 2;
        int res = 0;
        res += mergeSort(nums, left, mid);
        res += mergeSort(nums, mid + 1, right);
        res += merge(nums, left, mid, right);
        return res;
    }
    
    private int merge(int[] nums, int left, int mid, int right){
        int count = 0;
        int p = left, q = mid + 1;
        while (p <= mid && q <= right){
            if ((long) nums[p] > 2 * (long) nums[q]){
                count += mid - p + 1;
                q++;
            }
            else{
                p++;
            }
        }
        
        int[] temp = new int[right - left + 1];
        p = left; 
        q = mid + 1;
        int index = 0;
        while (p <= mid && q <= right){
            if (nums[p] > nums[q]){
                temp[index++] = nums[q++];
            }
            else{
                temp[index++] = nums[p++];
            }
        }
        while (p <= mid){
            temp[index++] = nums[p++];
        }
        while (q <= right){
            temp[index++] = nums[q++];
        }
        System.arraycopy(temp, 0, nums, left, right - left + 1);
        
        return count;
    }
}
```

<hr />