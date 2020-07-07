---
title: Leetcode473-matchsticksToSquare
categories: leetcode
tags: [DFS]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-12 23:04:09
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Remember the story of Little Match Girl? By now, you know exactly what matchsticks the little match girl has, please find out a way you can make one square by using up all those matchsticks. You should not break any stick, but you can link them up, and each matchstick must be used exactly one time.

Your input will be several matchsticks the girl has, represented with their stick length. Your output will either be true or false, to represent whether you could make one square using all the matchsticks the little match girl has.

## Example
**Example 1:**
```
Input: [1,1,2,2,2]
Output: true

Explanation: You can form a square with length 2, one side of the square came two sticks with length 1.
```
**Example 2:**
```
Input: [3,3,3,3,4]
Output: false

Explanation: You cannot find a way to form a square with all the matchsticks.
```
**Note:**
1. The length sum of the given matchsticks is in the range of 0 to 10^9.
2. The length of the given matchstick array will not exceed 15.

## Solution

**Solution 1:** DFS, but a little bit slow
```java
class Solution {
    public boolean makesquare(int[] nums) {
        if (nums.length < 4) return false;
        Arrays.sort(nums);
        int sum = 0;
        for (int stick: nums){
            sum += stick;
        }
        if (sum % 4 != 0) return false;
        return helper(nums, sum / 4, new int[4], nums.length-1);
    }
    private boolean helper(int[] nums, int target, int[] sticks, int index){
        if (index == -1){
            if (sticks[0] == target && sticks[1] == target && sticks[2] == target){
                return true;
            }
            return false;
        }
        for (int i = 0; i < 4; i++){
            if (sticks[i] + nums[index] > target) continue;
            sticks[i] += nums[index];
            if (helper(nums, target, sticks, index - 1)) return true;
            sticks[i] -= nums[index];
        }
        return false;
    }
}
```

**Solution 2:** Still DFS, but faster
```java
class Solution 
    public boolean makesquare(int[] nums) {
        if (nums.length < 4) return false;
        Arrays.sort(nums);
        int sum = 0;
        for (int stick: nums){
            sum += stick;
        }
        if (sum % 4 != 0) return false;
        boolean[] visited = new boolean[nums.length];
        return helper(nums, 0, nums.length - 1, sum / 4, visited, 4);
    }
    public boolean helper(int[] nums, int sum, int start, int target, boolean[] visited, int round){
        if (round == 0) return true;
        if (sum == target && helper(nums, 0, nums.length - 1, target, visited, round - 1)) 
            return true;
        for (int i = start; i >= 0; i--){
            if (!visited[i] && sum + nums[i] <= target){
                visited[i] = true;
                if (helper(nums, sum + nums[i], i -1, target, visited, round))
                    return true;
                visited[i] = false;
            }
        }
        return false;
    }
}
```
<hr />