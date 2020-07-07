---
title: Leetcode221-maximalSquare
categories: leetcode
tags: [DP, Google, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-28 11:35:54
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

## Example
```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```

## Solution
Method 1

dp[i][j] represents the length of the square which lower right corner is located at (i, j).

If the value of this cell is also 1, then the length of the square is the minimum of: the one above, its left, and diagonal up-left value +1. Because if one side is short or missing, it will not form a square.
```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if (matrix == null || matrix.length == 0) return 0;
        int m = matrix.length;
        int n = matrix[0].length;
        int[][] dp = new int[m + 1][n + 1];
        int res = 0;
        for (int i = 1; i <= m; i++){
            for (int j = 1; j <= n; j++){
                if (matrix[i - 1][j - 1] == '1'){
                    dp[i][j] = Math.min(Math.min(dp[i-1][j], dp[i][j-1]), dp[i-1][j-1]) + 1;
                    res = Math.max(res, dp[i][j] * dp[i][j]); 
                }
            }
        }
        return res;
    }
}
```

Method 2: More general, using Rectangle method
```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if (matrix == null || matrix.length == 0) return 0;
        int m = matrix.length;
        int n = matrix[0].length;
        int[] left = new int[n];
        int[] right = new int[n];
        int[] height = new int[n];
        Arrays.fill(left, 0);
        Arrays.fill(right, n - 1);
        Arrays.fill(height, 0);
        int res = 0;
        for (int i = 0; i < m; i++){
            int curLeft = 0;
            int curRight = n - 1;
            for(int j = 0; j < n; j++){
                if (matrix[i][j] == '1'){
                    height[j]++;
                    left[j] = Math.max(left[j], curLeft);
                }
                else{
                    height[j] = 0;
                    left[j] = 0;
                    curLeft = j + 1;
                }
            }          
            for (int j = n - 1; j >= 0; j--){
                if (matrix[i][j] == '1'){
                    right[j] = Math.min(right[j], curRight);
                }
                else{
                    right[j] = n - 1;
                    curRight = j - 1;
                }
                int len = Math.min(height[j], right[j] - left[j] + 1);
                res = Math.max(res, len * len);
            }
        }
        return res;
    }
}
```

<hr />