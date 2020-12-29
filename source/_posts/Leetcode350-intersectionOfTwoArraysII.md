---
title: Leetcode350-intersectionOfTwoArraysII
categories: leetcode
tags: [Hash Map, Two Pointers, Binary Search, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-12-25 18:39:54
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
Output: [2,2]
```
**Example 2:**
```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
```

**Note:**

* Each element in the result should appear as many times as it shows in both arrays.
* The result can be in any order.
**Follow up:**

* What if the given array is already sorted? How would you optimize your algorithm?
* What if nums1's size is small compared to nums2's size? Which algorithm is better?
* What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        HashMap<Integer, Integer> map = new HashMap<>();
        List<Integer> res = new ArrayList<>();
        for (int num: nums1){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        for (int num: nums2){
            if (map.containsKey(num) && map.get(num) > 0){
                map.put(num, map.get(num) - 1);
                res.add(num);
            }
        }
        int[] ans = new int[res.size()];
        for (int i = 0; i < res.size(); i++)
            ans[i] = res.get(i);
        return ans;
    }
}
```

**Follow up**

1. Two pointer iteration.
2. Let's say nums1 is K size. Then we should do binary search for every element in nums1. Each lookup is O(log N), and if we do K times, we have O(K log N). If K this is small enough, O(K log N) < O(max(N, M)). Otherwise, we have to use the previous two pointers method.
3. External Merge-Sort / MapReduced?

<hr />