---
title: Leetcode300-LongestIncreasingSubsequence
categories: leetcode
tags: [DP, Binary Search]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-20 23:13:08
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an unsorted array of integers, find the length of longest increasing subsequence.

## Example
```
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

**Note:**
* There may be more than one LIS combination, it is only necessary for you to return the length.
* Your algorithm should run in $O(n^2)$ complexity.

**Follow up:** Could you improve it to $O(n log n)$ time complexity?

## Solution

**Solution 1:** DP, $O(n^2)$
$$init: dp[i] = 1; (0 <= i < n)$$
$$dp[i] = max(dp[i], dp[j] + 1); (0 <= j < i, nums[j] < nums[i])$$
$$res = max(dp[i]); (0 <= i < n)$$
```java
class Solution {    
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int[] dp = new int[nums.length];
        for (int i = 0; i < nums.length; i++) dp[i] = 1;
        int res = 1;
        for (int i = 1; i < nums.length; i++){
            for (int j = 0; j < i; j++){
                if (nums[j] < nums[i])
                    dp[i] = Math.max(dp[i], dp[j] + 1);
            }
            res = Math.max(res, dp[i]);
        }
        return res;
    }
}
```

**Solution 2:** Binary Search + Greedy

Binary Search + Greedy, build one increasing queue

If new num > the last one in the queue, just add it.

If new num <= the last one, find the first num in the queue which <= the new num, replace it.  
```java
class Solution {    
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int[] incArray = new int[nums.length];
        incArray[0] = nums[0];
        int last = 0;
        for (int i = 1; i < nums.length; i++){
            if (nums[i] > incArray[last]){
                last++;
                incArray[last] = nums[i];
            }
            else{
                int temp = helper(incArray, 0, last, nums[i]);
                incArray[temp] = nums[i];
            }
        }
        return last + 1;
    }
    private int helper(int[] arr, int left, int right, int target){
        while(left < right){
            int mid = (left + right) / 2;
            if (arr[mid] == target) return mid;
            if (arr[mid] < target){
                left = mid + 1;
            }
            else right = mid;
        }
        return left;
    }
}
```
<hr />