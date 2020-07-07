---
title: Leetcode085-maximalRectangle
categories: leetcode
tags: [DP, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-13 10:56:43
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

## Example
```
Input:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
Output: 6
```

## Solution

The DP solution proceeds row by row, starting from the first row. Let the maximal rectangle area at row i and column j be computed by [right(i,j) - left(i,j)]*height(i,j).

All the 3 variables left, right, and height can be determined by the information from previous row, and also information from the current row. So it can be regarded as a DP solution. The transition equations are:

* left(i,j) = max(left(i-1,j), cur_left), cur_left can be determined from the current row

* right(i,j) = min(right(i-1,j), cur_right), cur_right can be determined from the current row

* height(i,j) = height(i-1,j) + 1, if matrix[i][j]=='1';

* height(i,j) = 0, if matrix[i][j]=='0'

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return 0;
        int m = matrix.length;
        int n = matrix[0].length;
        int[] left = new int[n];
        int[] right = new int[n];
        int[] height = new int[n];
        Arrays.fill(left, 0);
        Arrays.fill(right, n-1);
        Arrays.fill(height, 0);
        int res = 0;
        for (int i = 0; i < m; i++)
        {
            int curLeft = 0;
            int curRight = n - 1;
            for (int j = 0; j < n; j++){ 
                if (matrix[i][j] == '1'){
                    height[j] ++;   // compute height (can do this from either side)
                    left[j] = Math.max(left[j], curLeft);   // compute left (from left to right)
                }
                else{
                    height[j] = 0;
                    left[j] = 0;
                    curLeft = j + 1;
                }
            }
            for (int j = n - 1; j >= 0; j--){   // compute right (from right to left)
                if (matrix[i][j] == '1'){
                    right[j] = Math.min(right[j], curRight);
                }
                else{
                    right[j] = n - 1;
                    curRight = j - 1;
                }
                res = Math.max(res, (right[j] - left[j] + 1)*height[j]); // compute the area of rectangle (can do this from either side)
            }
        }
        return res;            
    }
}
```
<hr />