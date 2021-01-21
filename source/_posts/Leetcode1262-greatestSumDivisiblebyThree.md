---
title: Leetcode1262-Greatest Sum Divisible by Three
categories: leetcode
tags: [DP, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-10 18:11:57
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array nums of integers, we need to find the maximum possible sum of elements of the array such that it is divisible by three.

## Example

**Example 1:**
```
Input: nums = [3,6,5,1,8]
Output: 18
Explanation: Pick numbers 3, 6, 1 and 8 their sum is 18 (maximum sum divisible by 3).
```
**Example 2:**
```
Input: nums = [4]
Output: 0
Explanation: Since 4 is not divisible by 3, do not pick any number.
```
**Example 3:**
```
Input: nums = [1,2,3,4,4]
Output: 12
Explanation: Pick numbers 1, 3, 4 and 4 their sum is 12 (maximum sum divisible by 3).
``` 

**Constraints:**

* 1 <= nums.length <= 4 * 10^4
* 1 <= nums[i] <= 10^4

## Solution

```
 dp[i][m] = largest sum from a subset of nums[0..i - 1] such that the remainder of sum % 3 equals m
 dp[i][0] = max(dp[i - 1][0], dp[i - 1][0] + num[i]) when num[i] mod 3 == 0
 dp[i][1] = max(dp[i - 1][1], dp[i - 1][1] + num[i]) when num[i] mod 3 == 0
 dp[i][2] = max(dp[i - 1][2], dp[i - 1][2] + num[i]) when num[i] mod 3 == 0
    
 dp[i][0] = max(dp[i - 1][0], dp[i - 1][2] + num[i]) when num[i] mod 3 == 1
 dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + num[i]) when num[i] mod 3 == 1
 dp[i][2] = max(dp[i - 1][2], dp[i - 1][1] + num[i]) when num[i] mod 3 == 1

 dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] + num[i]) when num[i] mod 3 == 2
 dp[i][1] = max(dp[i - 1][1], dp[i - 1][2] + num[i]) when num[i] mod 3 == 2
 dp[i][2] = max(dp[i - 1][2], dp[i - 1][0] + num[i]) when num[i] mod 3 == 2

 Basic case
 dp[0][0] = 0
 dp[0][1] = -Inf   because 0 mod 3 == 1 is impossible
 dp[0][2] = -Inf   because 0 mod 3 == 2 is impossible

 dp[i][j] is only based on dp[i - 1][j], could use 1-D array to store dp.
```

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(1)$$

### Solution 1: 1-D Array

```java
class Solution {
    public int maxSumDivThree(int[] nums) {
        int[] dp = new int[3];
        dp[1] = Integer.MIN_VALUE;
        dp[2] = Integer.MIN_VALUE;
        
        for (int num : nums){
            int[] temp = Arrays.copyOf(dp, dp.length);
            int remainder = num % 3;
            if (remainder == 0){
                temp[0] = Math.max(dp[0], num + dp[0]);
                temp[1] = Math.max(dp[1], num + dp[1]);
                temp[2] = Math.max(dp[2], num + dp[2]);
            }
            else if (remainder == 1){
                temp[0] = Math.max(dp[0], num + dp[2]);
                temp[1] = Math.max(dp[1], num + dp[0]);
                temp[2] = Math.max(dp[2], num + dp[1]);
                
            }
            else if (remainder == 2){
                temp[0] = Math.max(dp[0], num + dp[1]);
                temp[1] = Math.max(dp[1], num + dp[2]);
                temp[2] = Math.max(dp[2], num + dp[0]);
            }
            dp = temp;
        }
        return dp[0];
    }
}
```

### Solution 2: Clean 1-D Array
```java
class Solution {
    public int maxSumDivThree(int[] nums) {
        int[] dp = new int[3];
        dp[1] = Integer.MIN_VALUE;
        dp[2] = Integer.MIN_VALUE;
        
        for (int num : nums){
            int[] temp = Arrays.copyOf(dp, dp.length);
            int remainder = num % 3;
            for (int i = 0; i < 3; i++) {
                temp[i] = Math.max(dp[i], dp[(i + 3 - remainder) % 3] + num);
            }
            dp = temp;
        }
        return dp[0];
    }
}
```

### Solution 3: Follow up - divided by K
* Time Complexity: $$O(N)$$
* Space Complexity: $$O(K)$$
```java
class Solution {
    public int maxSumDivThree(int[] nums){
        return helper(nums, 3);
    }
    public int helper(int[] nums, int k) {
        int[] dp = new int[k];
        for (int i = 1; i < k; i++)
            dp[i] = Integer.MIN_VALUE;
        
        for (int num : nums){
            int[] temp = Arrays.copyOf(dp, dp.length);
            int remainder = num % k;
            for (int i = 0; i < k; i++) {
                temp[i] = Math.max(dp[i], dp[(i + k - remainder) % k] + num);
            }
            dp = temp;
        }
        return dp[0];
    }
}
```

<hr />