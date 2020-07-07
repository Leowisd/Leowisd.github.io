---
title: Leetcode532-k-diffPairsInAnArray
categories: leetcode
tags: [Hash Table, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-26 17:27:22
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

## Description
Given an array of integers and an integer k, you need to find the number of unique k-diff pairs in the array. Here a k-diff pair is defined as an integer pair (i, j), where i and j are both numbers in the array and their absolute difference is k.

## Example
**Example 1:**
````
Input: [3, 1, 4, 1, 5], k = 2
Output: 2
Explanation: There are two 2-diff pairs in the array, (1, 3) and (3, 5).
Although we have two 1s in the input, we should only return the number of unique pairs.
```
**Example 2:**
```
Input:[1, 2, 3, 4, 5], k = 1
Output: 4
Explanation: There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).
```
**Example 3:**
```
Input: [1, 3, 1, 5, 4], k = 0
Output: 1
Explanation: There is one 0-diff pair in the array, (1, 1).
```
**Note:**
The pairs (i, j) and (j, i) count as the same pair.
The length of the array won't exceed 10,000.
All the integers in the given input belong to the range: [-1e7, 1e7].

## Solution
```java
class Solution {
    public int findPairs(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k < 0) return 0;
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int it: nums){
            map.put(it, map.getOrDefault(it, 0)+1);
        }
        
        int res = 0;
        for (int it: map.keySet()){
            if (k == 0){
                if (map.get(it) > 1) res++;
            }
            else {
                if (map.containsKey(it + k)) res ++;
            }
        }
        
        return res;
    }
}
```

<hr />