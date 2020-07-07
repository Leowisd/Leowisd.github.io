---
title: Leetcode018-4Sum
categories: leetcode
tags: [Two Pointers]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-10 22:39:50
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array nums of n integers and an integer target, are there elements a, b, c, and d in nums such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

**Note:**

The solution set must not contain duplicate quadruplets.

## Example
```
Given array nums = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

## Solution
```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> res = new ArrayList<>();
        int i = 0;
        Arrays.sort(nums);
        while (i < nums.length - 3){
            int j = i + 1;
            while (j < nums.length - 2){
                List<List<Integer>> tmp = twoSum(nums, j + 1, target-nums[i]-nums[j]);
                if (tmp.size() > 0){
                    for (List<Integer> t : tmp){
                        t.add(nums[i]);
                        t.add(nums[j]);
                        res.add(t);
                    }
                }
                j ++;
                while (j < nums.length - 2 && nums[j] == nums[j-1]) j++;
            }
            i++;
            while(i < nums.length - 3 && nums[i] == nums[i-1]) i++;
        }
        return res;
    }
    private List<List<Integer>> twoSum(int[] nums, int i, int target){
        int j = nums.length - 1;
        List<List<Integer>> res = new ArrayList<>();
        while (i < j){
            if (nums[i] + nums[j] == target){
                List<Integer> tmp = new ArrayList<>();
                tmp.add(nums[i]);
                tmp.add(nums[j]);
                res.add(tmp);
                
                i++;
                j--;
                while(i < j && nums[i] == nums[i-1]) i++;
                while(i < j && nums[j] == nums[j+1]) j--;
            }
            else if (nums[i] + nums[j] < target) i++;
            else j--;
        }
        return res;
    }
}
```

<hr />