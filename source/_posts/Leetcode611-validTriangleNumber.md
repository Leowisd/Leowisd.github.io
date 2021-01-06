---
title: Leetcode611-validTriangleNumber
categories: leetcode
tags: [Array, Two Pointers, Bloomberg, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 15:17:23
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

## Example
```
Input: [2,2,3,4]
Output: 3
Explanation:
Valid combinations are: 
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3
```

**Note:**
1. The length of the given array won't exceed 1000.
2. The integers in the given array are in the range of [0, 1000].

## Solution
```java
class Solution {
    public int triangleNumber(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        Arrays.sort(nums);
        int res = 0;
        for (int i = 2; i < nums.length; i++){
            int left = 0;
            int right = i - 1;
            while(left < right){
                if (nums[left] + nums[right] > nums[i]){
                    res += right - left;
                    right--;
                }
                else
                    left++;
            }
        }
        return res;
    }
}
```

<hr />