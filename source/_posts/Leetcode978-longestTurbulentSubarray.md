---
title: Leetcode978-longestTurbulentSubarray
categories: leetcode
tags: [Array, DP, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-29 23:50:41
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

A subarray A[i], A[i+1], ..., A[j] of A is said to be turbulent if and only if:

* For i <= k < j, A[k] > A[k+1] when k is odd, and A[k] < A[k+1] when k is even;
* OR, for i <= k < j, A[k] > A[k+1] when k is even, and A[k] < A[k+1] when k is odd.

That is, the subarray is turbulent if the comparison sign flips between each adjacent pair of elements in the subarray.

Return the length of a maximum size turbulent subarray of A.

## Example
**Example 1:**
```
Input: [9,4,2,10,7,8,8,1,9]
Output: 5
Explanation: (A[1] > A[2] < A[3] > A[4] < A[5])
```
**Example 2:**
```
Input: [4,8,12,16]
Output: 2
```
**Example 3:**
```
Input: [100]
Output: 1
```
**Note:**

1. 1 <= A.length <= 40000
2. 0 <= A[i] <= 10^9

## Solution
**Solutio 1:** Basic solution, Time O(n), Space O(n)
```java
class Solution {
//  Basic Method: Time: O(n), Space: O(n)
//     For each A[i]
//  inc: The length of current valid sequence which ends with two increasing numbers
//  dec: The length of current valid sequence which ends with two decreasing numbers
    public int maxTurbulenceSize(int[] A) {
        if (A == null || A.length == 0)
            return 0;
        int[] inc = new int[A.length];
        int[] des = new int[A.length];
        int res = 1;
        Arrays.fill(inc, 1);
        Arrays.fill(des, 1);
        
        for (int i = 1; i < A.length; i++){
            if (A[i] > A[i - 1])
                inc[i] = des[i - 1] + 1;
            else if (A[i] < A[i - 1])
                des[i] = inc[i - 1] + 1;
            
            res = Math.max(res, Math.max(inc[i], des[i]));
        }
        return res;
    }
}
```

**Solution 2:** Improved Solution, Space O(1)
```java
class Solution {
//  Improved: O(1) Space; O(N) time
    public int maxTurbulenceSize(int[] A) {
        if (A == null || A.length == 0)
            return 0;
        int res = 1;
        int inc = 1;
        int des = 1;
        for (int i = 1; i < A.length; i++){
            if (A[i] > A[i - 1]){
                inc = des + 1;
                des = 1;
            }
            else if (A[i] < A[i - 1]){
                des = inc + 1;
                inc = 1;
            }
            else{
                inc = 1;
                des = 1;
            }
            res = Math.max(res, Math.max(inc, des));
        }
        return res;
    }
}
```

<hr />