---
title: Leetcode152-Maximum Product Subarray
categories: leetcode
tags: [DP, Linkedin]
description: Solution Report of LeetCode Accepted
mathjax: true
date: 2022-01-25 14:34:09
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an integer array nums, find a contiguous non-empty subarray within the array that has the largest product, and return the product.

The test cases are generated so that the answer will fit in a 32-bit integer.

A subarray is a contiguous subsequence of the array.

## Example

**Example 1:**
```
Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```
**Example 2:**
```
Input: nums = [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```
**Constraints:**

* 1 <= nums.length <= 2 * 104
* -10 <= nums[i] <= 10
* The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

## Solution

**Solution 1: DP**

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(1)$$

```java
class Solution {
//    DP
// dp[i][0] = min( min(dp[i - 1][0] * nums[i], dp[i - 1][1] * nums[i]), nums[i])
// dp[i][1] = max( max(dp[i - 1][0] * nums[i], dp[i - 1][1] * nums[i]), nums[i])
// improved:
// minPro = min( min(minPro * nums[i], maxPro * nums[i]), nums[i])
// maxPro = max( max(minPro * nums[i], maxPro * nums[i]), nums[i])
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        
        int premax = nums[0], premin = nums[0];
        int min = 0, max = 0;
        int res = premax;
        for (int i = 1; i < nums.length; i++){
            min = premin * nums[i];
            max = premax * nums[i];
            premax = Math.max(Math.max(min, max), nums[i]);
            premin = Math.min(Math.min(min, max), nums[i]);
            res = Math.max(res, premax);            
        }
        return res;
    }
}
```

**Solution 2: cal prefix and suffix**

```java
//    Solution 2: cal prefix and suffix 
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int res = nums[0];
        int prefix = 0, suffix = 0;
        for (int i = 0; i < nums.length; i++){
            prefix = (prefix == 0 ? 1 : prefix) * nums[i];
            suffix = (suffix == 0 ? 1 : suffix) * nums[nums.length - i - 1];
            res = Math.max(res, Math.max(prefix, suffix));
        }
        return res;
    }
```

<hr />