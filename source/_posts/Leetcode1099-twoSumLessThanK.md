---
title: Leetcode1099-twoSumLessThanK
categories: leetcode
tags: [Array, Two Pointers, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-08 20:01:45
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array A of integers and integer K, return the maximum S such that there exists i < j with A[i] + A[j] = S and S < K. If no i, j exist satisfying this equation, return -1.

## Example
**Example 1:**
```
Input: A = [34,23,1,24,75,33,54,8], K = 60
Output: 58
Explanation: 
We can use 34 and 24 to sum 58 which is less than 60.
```
**Example 2:**
```
Input: A = [10,20,30], K = 15
Output: -1
Explanation: 
In this case it's not possible to get a pair sum less that 15.
```
## Solution
```java
class Solution {
    public int twoSumLessThanK(int[] A, int K) {
        if (A == null || A.length == 0) return -1;
        
        Arrays.sort(A);
        int i = 0;
        int j = A.length - 1;
        int res = Integer.MIN_VALUE;
        while(i<j){
            if (A[i] + A[j] >= K){
                j--;
            }
            else{
                res = Math.max(res, A[i] + A[j]);
                i++;
            }
        }
        if (res == Integer.MIN_VALUE) return -1;
        return res;
    }
}
// class Solution {
//     public int twoSumLessThanK(int[] A, int K) {
//         TreeSet<Integer> set = new TreeSet<>();
//         int res = -1;
//         for (int a : A) {
//             Integer pre = set.lower(K - a);
//             if (pre != null) {
//                 res = Math.max(res, a + pre);
//             }
//             set.add(a);
//         }
//         return res;
//     }
// }
```

<hr />