---
title: Leetcode363-maxSumOfRectangleNoLargerThanK
categories: leetcode
tags: [DP, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 17:26:12
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a non-empty 2D matrix matrix and an integer k, find the max sum of a rectangle in the matrix such that its sum is no larger than k.

## Example
```
Input: matrix = [[1,0,1],[0,-2,3]], k = 2
Output: 2 
Explanation: Because the sum of rectangle [[0, 1], [-2, 3]] is 2,
             and 2 is the max number no larger than k (k = 2).
```

**Note:**

1. The rectangle inside the matrix must have an area > 0.
2. What if the number of rows is much larger than the number of columns?

## Solution
**Solution 1: Brute force**
```java
class Solution {
    // O((nm)^2)     
    public int maxSumSubmatrix(int[][] matrix, int k) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return 0;
        int rows = matrix.length, cols = matrix[0].length;
        int[][] areas = new int[rows][cols];
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                int area = matrix[r][c];
                if (r-1 >= 0)
                    area += areas[r-1][c];
                if (c-1 >= 0)
                    area += areas[r][c-1];
                if (r-1 >= 0 && c-1 >= 0)
                    area -= areas[r-1][c-1];
                areas[r][c] = area;
            }
        }
        int max = Integer.MIN_VALUE;
        for (int r1 = 0; r1 < rows; r1++) {
            for (int c1 = 0; c1 < cols; c1++) {
                for (int r2 = r1; r2 < rows; r2++) {
                    for (int c2 = c1; c2 < cols; c2++) {
                        int area = areas[r2][c2];
                        if (r1-1 >= 0)
                            area -= areas[r1-1][c2];
                        if (c1-1 >= 0)
                            area -= areas[r2][c1-1];
                        if (r1-1 >= 0 && c1 -1 >= 0)
                            area += areas[r1-1][c1-1];
                        if (area <= k)
                            max = Math.max(max, area);
                    }
                }
            }
        }
        return max;
    }
}
```
**Solution 2: 2D Kadane's algorithm + 1D maxSum problem with sum limit k**
```java
class Solution {
//     O(n^2 * m * logm)
    public int maxSumSubmatrix(int[][] matrix, int k) {
        //2D Kadane's algorithm + 1D maxSum problem with sum limit k
        //2D subarray sum solution

        //boundary check
        if(matrix.length == 0) return 0;

        int m = matrix.length, n = matrix[0].length;
        int result = Integer.MIN_VALUE;

        //outer loop should use smaller axis
        //now we assume we have more rows than cols, therefore outer loop will be based on cols 
        for(int left = 0; left < n; left++){
            //array that accumulate sums for each row from left to right 
            int[] sums = new int[m];
            for(int right = left; right < n; right++){
                //update sums[] to include values in curr right col
                for(int i = 0; i < m; i++){
                    sums[i] += matrix[i][right];
                }

                //we use TreeSet to help us find the rectangle with maxSum <= k with O(logN) time
                TreeSet<Integer> set = new TreeSet<Integer>();
                //add 0 to cover the single row case
                set.add(0);
                int currSum = 0;

                for(int sum : sums){
                    currSum += sum;
                    //we use sum subtraction (curSum - sum) to get the subarray with sum <= k
                    //therefore we need to look for the smallest sum >= currSum - k
                    Integer num = set.ceiling(currSum - k);
                    if(num != null) result = Math.max( result, currSum - num );
                    set.add(currSum);
                }
            }
        }

        return result;
    }
}
```

<hr />