---
title: Leetcode015-3Sum
categories: leetcode
tags: [Array, Two Pointers, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-04 11:02:10
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

## Example
```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## Solution
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length == 0) return res;
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i ++){
            if (i > 0 && nums[i] == nums[i-1]) continue;
            if (nums[i] > 0) break;
            int j = i + 1;
            int k = nums.length-1;
            while (j < k){
                if (nums[i] + nums[j] + nums[k] == 0){
                    List<Integer> tmp = new ArrayList<>();
                    tmp.add(nums[i]);
                    tmp.add(nums[j]);
                    tmp.add(nums[k]);
                    res.add(tmp);
                    j++;
                    while (j < k && nums[j] == nums[j-1]) j++;
                    k--;
                    while (j < k && nums[k] == nums[k+1]) k--;
                }
                else if (nums[i] + nums[j] + nums[k] < 0){
                    j++;
                    while (j < k && nums[j] == nums[j-1]) j++;
                }
                else if (nums[i] + nums[j] + nums[k] > 0){
                    k--;
                    while (j < k && nums[k] == nums[k+1]) k--;
                }
            }
        }
        return res;
    }
}
```
Time Complex: $O(N^2)$

<hr />