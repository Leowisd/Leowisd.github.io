---
title: Leetcode1000-minimumCostToMergeStones
categories: leetcode
tags: [DP, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-07 17:58:58
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

There are N piles of stones arranged in a row.  The i-th pile has stones[i] stones.

A move consists of merging exactly K consecutive piles into one pile, and the cost of this move is equal to the total number of stones in these K piles.

Find the minimum cost to merge all piles of stones into one pile.  If it is impossible, return -1.

## Example
**Example 1:**
```
Input: stones = [3,2,4,1], K = 2
Output: 20
Explanation: 
We start with [3, 2, 4, 1].
We merge [3, 2] for a cost of 5, and we are left with [5, 4, 1].
We merge [4, 1] for a cost of 5, and we are left with [5, 5].
We merge [5, 5] for a cost of 10, and we are left with [10].
The total cost was 20, and this is the minimum possible.
```
**Example 2:**
```
Input: stones = [3,2,4,1], K = 3
Output: -1
Explanation: After any merge operation, there are 2 piles left, and we can't merge anymore.  So the task is impossible.
```
**Example 3:**
```
Input: stones = [3,5,1,2,6], K = 3
Output: 25
Explanation: 
We start with [3, 5, 1, 2, 6].
We merge [5, 1, 2] for a cost of 8, and we are left with [3, 8, 6].
We merge [3, 8, 6] for a cost of 17, and we are left with [17].
The total cost was 25, and this is the minimum possible.
```
**Note:**

* 1 <= stones.length <= 30
* 2 <= K <= 30
* 1 <= stones[i] <= 100

## Solution
```java
class Solution {
    public int mergeStones(int[] stones, int K) {
        int len = stones.length;
        if ((len - 1) % (K - 1) != 0) {
            return -1;
        }
        
        int i, j, k, l, t;
        
        int[] prefixSum = new int[len + 1];
        for (i = 1; i <= len; i++) {
            prefixSum[i] = prefixSum[i - 1] + stones[i - 1];
        }
        
        int max = 99999999;
        int[][][] dp = new int[len + 1][len + 1][K + 1];
        for (i = 1; i <= len; i++) {
            for (j = 1; j <= len; j++) {
                for (k = 1; k <= K; k++) {
                    dp[i][j][k] = max;
                }
            }
        }
        
        for (i = 1; i <= len; i++) {
            dp[i][i][1] = 0;
        }

        for (l = 2; l <= len; l++) {
            for (i = 1; i <= len - l + 1; i++) {
                j = i + l - 1;
                for (k = 2; k <= K; k++) {
                    for (t = i; t < j; t++) {
                        dp[i][j][k] = Math.min(dp[i][j][k], dp[i][t][k - 1] + dp[t + 1][j][1]);
                    }
                }

                dp[i][j][1] = dp[i][j][K] + prefixSum[j] - prefixSum[i - 1];   
            }
        }

        return dp[1][len][1];
    }
}

// class Solution {
//     public int mergeStones(int[] stones, int K) {
//         if (stones.length < K) return -1;
        
//         int len = stones.length - K + 1;
//         int[] window = new int[len];
        
//         int itr = 0;
//         int min = Integer.MAX_VALUE;
//         int index = -1;
//         for (int i = 0; i < stones.length; i++){
//             if (i >= K){
//                 if (min > window[itr]){
//                     min = window[itr];
//                     index= itr;
//                 }
//                 itr ++;
//                 window[itr] = window[itr-1] - stones[i-K] + stones[i];
//             }
//             else window[itr] += stones[i];
//         }
//         if (min > window[itr]){
//             min = window[itr];
//             index= itr;
//         }
        
//         int newLen = stones.length - K + 1;
        
//         int[] newS = new int[newLen];
//         int j = 0;
//         for (int i = 0; i < stones.length; i++){
//             if (i == index) newS[j] = min;
//             else if (i> index && i < index + K) continue;
//             else {
//                 newS[j] = stones[i];
//             }
//             j++;
//         }
        
//         int get;
//         if (newLen == 1) return newS[0]; 
//         else get = mergeStones(newS, K);
        
//         if (get == -1) return -1;
//         return get + min;
//     }
// }
```

<hr />