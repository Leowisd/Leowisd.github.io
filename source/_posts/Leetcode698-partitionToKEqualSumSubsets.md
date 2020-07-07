---
title: Leetcode698-partitionToKEqualSumSubsets
categories: leetcode
tags: [DFS]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-12 23:54:05
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers nums and a positive integer k, find whether it's possible to divide this array into k non-empty subsets whose sums are all equal.

## Example
```
Input: nums = [4, 3, 2, 3, 5, 2, 1], k = 4
Output: True
Explanation: It's possible to divide it into 4 subsets (5), (1, 4), (2,3), (2,3) with equal sums.
```
**Note:**

* 1 <= k <= len(nums) <= 16.
* 0 < nums[i] < 10000.

## Solution
Solution 1: DFS, but slower
```java
class Solution {
    public boolean canPartitionKSubsets(int[] nums, int k) {
        if (nums.length < k) return false;
        Arrays.sort(nums);
        int sum = 0;
        for (int num: nums) sum += num;
        if (sum % k != 0) return false;
        return helper(nums, sum / k, new int[k], nums.length-1);
    }
    public boolean helper(int[] nums, int target, int[] parts, int index){
        if (index == -1){
            boolean flag = true;
            for (int part: parts){
                if (part != target){
                    flag = false;
                    break;
                }
            }
            return flag;
        }
        for (int i = 0; i < parts.length; i++){
            if (parts[i] + nums[index] > target) continue;
            parts[i] += nums[index];
            if (helper(nums, target, parts, index - 1)) return true;
            parts[i] -= nums[index];
        }
        return false;
    }
}
```

Solution 2: Still DFS, but faster
```java
class Solution {
    public boolean canPartitionKSubsets(int[] A, int k) {
        if (k > A.length) return false;
        int sum = 0;
        for (int num : A) sum += num;
        if (sum % k != 0) return false;
        boolean[] visited = new boolean[A.length];
        Arrays.sort(A);
        return helper(A, 0, A.length - 1, visited, sum / k, k);
    }

    public boolean helper(int[] A, int sum, int st, boolean[] visited, int target, int round) {
        if (round == 0) return true;
        if (sum == target && helper(A, 0, A.length - 1, visited, target, round - 1))
            return true;
        for (int i = st; i >= 0; --i) {
            if (!visited[i] && sum + A[i] <= target) {
                visited[i] = true;
                if (helper(A, sum + A[i], i - 1, visited, target, round))
                    return true;
                visited[i] = false;
            }
        }
        return false;
    }
}
```

<hr />