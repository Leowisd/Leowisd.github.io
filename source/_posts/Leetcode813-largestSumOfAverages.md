---
title: Leetcode813-largestSumOfAverages
categories: leetcode
tags: [DP, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-29 23:54:01
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

We partition a row of numbers A into at most K adjacent (non-empty) groups, then our score is the sum of the average of each group. What is the largest score we can achieve?

Note that our partition must use every number in A, and that scores are not necessarily integers.

## Example
```
Input: 
A = [9,1,2,3,9]
K = 3
Output: 20
Explanation: 
The best choice is to partition A into [9], [1, 2, 3], [9]. The answer is 9 + (1 + 2 + 3) / 3 + 9 = 20.
We could have also partitioned A into [9, 1], [2], [3, 9], for example.
That partition would lead to a score of 5 + 2 + 6 = 13, which is worse.
```

**Note:**

* 1 <= A.length <= 100.
* 1 <= A[i] <= 10000.
* 1 <= K <= A.length.
* Answers within 10^-6 of the correct answer will be accepted as correct.

## Solution
```java
// search return the result for n first numbers to k groups.
// Time complexity: O(KN^2)
class Solution {
    public double largestSumOfAverages(int[] A, int K) {
        int N = A.length;
        double[][] memo = new double[N+1][N+1];
        double cur = 0;
        for (int i = 0; i < N; ++i) {
            cur += A[i];
            memo[i + 1][1] = cur / (i + 1);
        }
        return search(N, K, A, memo);
    }
    
    public double search(int n, int k, int[] A, double[][] memo) {
        if (memo[n][k] > 0) return memo[n][k];
        if (n < k) return 0;
        double cur = 0;
        for (int i = n - 1; i > 0; --i) {
            cur += A[i];
            memo[n][k] = Math.max(memo[n][k], search(i, k - 1, A, memo) + cur / (n - i));
        }
        return memo[n][k];
    }
}
```

<hr />