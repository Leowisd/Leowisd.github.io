---
title: Leetcode240-searchA2DMatrixII
categories: leetcode
tags: [Matrix, Amazon, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-22 17:01:33
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.

## Example
```
Consider the following matrix:

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
Given target = 5, return true.

Given target = 20, return false.
```

## Solution
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return false;
        
        int n = matrix.length;
        int m = matrix[0].length;
        int i = 0, j = m - 1;
        while (i>=0 && i < n && j >=0 && j < m){
            if (matrix[i][j] == target) return true;
            if (matrix[i][j] < target ) i++;
            else j --;
        }
        return false;
    }
}
```

<hr />