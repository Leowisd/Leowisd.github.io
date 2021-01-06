---
title: Leetcode977-Squares of a Sorted Array
categories: leetcode
tags: [Array, Two Pointers, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-05 23:17:34
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

## Example

**Example 1:**
```
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```
**Example 2:**
```
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```

**Constraints:**

* 1 <= nums.length <= 104
* -104 <= nums[i] <= 104
* nums is sorted in non-decreasing order.

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

```java
class Solution {
    public int[] sortedSquares(int[] A) {
        if (A == null || A.length == 0) return A;
        int[] res = new int[A.length];
        int idx = A.length - 1;
        int left = 0;
        int right = A.length - 1;
        while(left <= right){
            if (Math.abs(A[left]) > Math.abs(A[right])){
                res[idx] = A[left] * A[left];
                left++;
            }
            else{
                res[idx] = A[right] * A[right];
                right--;
            }
            idx--;
        }
        
        return res;
    }
}
```

<hr />