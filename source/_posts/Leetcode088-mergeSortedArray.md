---
title: Leetcode088-mergeSortedArray
categories: leetcode
tags: [Array, Two Pointers, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 22:23:17
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array

**Note:**

* The number of elements initialized in nums1 and nums2 are m and n respectively.
* You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.

## Example
```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

## Solution

**Solution: best solution**
```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n -1;
        while (i >= 0 && j >= 0){
            if (nums1[i] > nums2[j]){
                nums1[k--] = nums1[i--];
            }
            else
                nums1[k--] = nums2[j--];
        }
        while (i >= 0)
            nums1[k--] = nums1[i--];
        while (j >= 0)
            nums1[k--] = nums2[j--];
    }
}
```

**Solution 2: Not a good solution**
```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        if (n == 0) return;
        int[] tmp = new int[n + m];
        int i = 0;
        int j = 0;
        int index = 0;
        while (i < m && j < n){
            if (nums1[i] <= nums2[j]){
                tmp[index++] = nums1[i++];
            }
            else{
                tmp[index++] = nums2[j++];
            }
        }
        if (i < m)
            for (int k = i; i < m; k++) tmp[index++] = nums1[i++];
        if (j < n)
            for (int k = j; j < n; k++) tmp[index++] = nums2[j++];
        for (int k = 0; k < m + n; k++)
            nums1[k] = tmp[k];
    }
}
```

<hr />