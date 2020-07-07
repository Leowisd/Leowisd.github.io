---
title: Leetcode209-minimumSizeSubarraySum
categories: leetcode
tags: [Array, Two Pointers, Binary Search, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-28 15:41:44
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.

## Example
```
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```
**Follow up:**

If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log n). 

## Solution

**Solution 1:** Two Pointers, O(N)

```java
class Solution {
// Two Pointers, O(n)
    public int minSubArrayLen(int s, int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int left = 0, right = 0;
        int res = Integer.MAX_VALUE;
        int cur = 0;
        while(right < nums.length){
            cur += nums[right];
            if(cur < s){
                right++;
            }
            else{
                while(cur >= s){
                    res = Math.min(res, right - left + 1);
                    cur -= nums[left];
                    left++;
                }
                right++;
            }
        }
        return res == Integer.MAX_VALUE ? 0 : res;
    }
}
```
**Solution 2:** Follow up, Bianry search, O(NlogN)
```java
class Solution {
//     O(NlongN): bianry search
    public int minSubArrayLen(int s, int[] nums) {
        int[] sums = new int[nums.length + 1];
        for (int i = 1; i < sums.length; i++) sums[i] = sums[i - 1] + nums[i - 1];
        int minLen = Integer.MAX_VALUE;
        for (int i = 0; i < sums.length; i++) {
            int end = binarySearch(i + 1, sums.length - 1, sums[i] + s, sums);
            if (end == sums.length) break;
            if (end - i < minLen) minLen = end - i;
        }
        return minLen == Integer.MAX_VALUE ? 0 : minLen;
    }
    private int binarySearch(int lo, int hi, int key, int[] sums) {
        while (lo <= hi) {
           int mid = (lo + hi) / 2;
           if (sums[mid] >= key){
               hi = mid - 1;
           } else {
               lo = mid + 1;
           }
        }
        return lo;
    }
}
```

<hr />