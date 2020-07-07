---
title: Leetcode1060-missingElementinSortedArray
categories: leetcode
tags: [Binary Search, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 00:40:02
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a sorted array A of unique numbers, find the K-th missing number starting from the leftmost number of the array.

## Example
**Example 1:**
```
Input: A = [4,7,9,10], K = 1
Output: 5
Explanation: 
The first missing number is 5.
```
**Example 2:**
```
Input: A = [4,7,9,10], K = 3
Output: 8
Explanation: 
The missing numbers are [5,6,8,...], hence the third missing number is 8.
```
**Example 3:**
```
Input: A = [1,2,4], K = 3
Output: 6
Explanation: 
The missing numbers are [3,5,6,7,...], hence the third missing number is 6.
```

## Solution
Let missingNum be the number of missing number in the array. Two cases that need to be handled:

missingNum < k, then return nums[n - 1] + k - missingNum
missingNum >= k, then use binary search(during the search k will be updated) to find the index in the array, where the kth missing number will be located in (nums[index], nums[index + 1]), return nums[index] + k
```java
class Solution {
    public int missingElement(int[] nums, int k) {
        int n = nums.length;
        int l = 0;
        int h = n - 1;
        int missingNum = nums[n - 1] - nums[0] - (n - 1);
        
        if (missingNum < k)
            return nums[n - 1] + k - missingNum;
        
        while(l < h - 1){
            int mid = (h + l)/2;
            int missingN = nums[mid] - nums[l] - (mid - l);
            
            if (missingN >= k){
                // when the number is larger than k, then the index won't be located in (m, h]
                h = mid;
            }
            else{
                // when the number is smaller than k, then the index won't be located in [l, m), update k -= missing
                k -= missingN;
                l = mid;
            }
        }
        return nums[l] + k;
    }
}
```

<hr />