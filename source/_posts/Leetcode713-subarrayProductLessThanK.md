---
title: Leetcode713-subarrayProductLessThanK
categories: leetcode
tags: [Array, Two Pointers, Sliding Window]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-30 10:12:15
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Your are given an array of positive integers nums.

Count and print the number of (contiguous) subarrays where the product of all the elements in the subarray is less than k.

## Example
```
Input: nums = [10, 5, 2, 6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are: [10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6].
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.
```
**Note:**

* 0 < nums.length <= 50000.
* 0 < nums[i] < 1000.
* 0 <= k < 10^6.

## Solution
```java
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        if (k == 0) return 0;
        int res = 0;
        int i = 0;
        int j = 0;
        int product = 1;
        while(j < nums.length){
            product *= nums[j];
            while(i <= j && product >= k){
                product /= nums[i];
                i++;
            }
            res += j - i + 1;
            j++;
        }
        return res;
    }
}
```

<hr />