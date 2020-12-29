---
title: leetcode349-Intersection Of Two Arrays
categories: leetcode
tags: [Hash Table, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-12-27 18:05:23
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given two arrays, write a function to compute their intersection.

## Example
**Example 1:**
```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```
**Example 2:**
```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
```
**Note:**

* Each element in the result must be unique.
* The result can be in any order.

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1.length == 0 || nums2.length == 0) return new int[0];
        HashSet<Integer> set = new HashSet<>();
        for (int num: nums1){
            set.add(num);
        }
        List<Integer> tmp = new ArrayList<>();
        for (int num: nums2){
            if (set.contains(num)){
                tmp.add(num);
                set.remove(num);
            }
        }
        int[] res = new int[tmp.size()];
        for (int i = 0; i < tmp.size(); i++){
            res[i] = tmp.get(i);
        }
        return res;
    }
}
```

<hr />