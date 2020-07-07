---
title: Leetcode054-spiralMatrix
categories: leetcode
tags: [Array, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-21 14:23:22
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

## Example
**Example 1:**
```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
```
**Example 2:**
```
Input:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

## Solution
```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return res;
        
        int m = matrix.length;
        int n = matrix[0].length;       
        int i = 0;
        int j = 0;
        int direction = 0;
        int[][] dir = new int[][]{{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        boolean[][] visited = new boolean[m][n];
        while (res.size() < n * m){
            res.add(matrix[i][j]);
            if (res.size() == n * m) break;
            visited[i][j] = true;
            int ni = i + dir[direction][0];
            int nj = j + dir[direction][1];
            while( ni >= m || nj >= n || ni < 0 || nj < 0 || visited[ni][nj]){
                direction ++;
                if (direction > 3) direction = 0;
                ni = i + dir[direction][0];
                nj = j + dir[direction][1];
            }
            i = ni;
            j = nj;
        }        
        return res;
    }
}
```

<hr />