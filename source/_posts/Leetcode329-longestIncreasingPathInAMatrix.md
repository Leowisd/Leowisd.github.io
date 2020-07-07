---
title: Leetcode329-longestIncreasingPathInAMatrix
categories: leetcode
tags: [DFS, Bloomberg, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 21:27:10
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an integer matrix, find the length of the longest increasing path.

From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary (i.e. wrap-around is not allowed).

## Example
**Example 1:**
```
Input: nums = 
[
  [9,9,4],
  [6,6,8],
  [2,1,1]
] 
Output: 4 
Explanation: The longest increasing path is [1, 2, 6, 9].
```

**Example 2:**
```
Input: nums = 
[
  [3,4,5],
  [3,2,6],
  [2,2,1]
] 
Output: 4 
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.
```

## Solution

DFS with memory

```java
class Solution {
    private int[][] dir = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    public int longestIncreasingPath(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return 0;
        
        int res = 0;
        int[][] memory = new int[matrix.length][matrix[0].length];
        for (int i = 0; i < matrix.length; i++){
            for (int j = 0; j < matrix[0].length; j++){
                if (memory[i][j] == 0){
                    res = Math.max(res, helper(matrix, i, j, memory));
                }
            }
        }
        
        return res;
    }
    
    private int helper(int[][] matrix, int x, int y, int[][] memory){
        for (int i = 0 ; i < dir.length; i++){
            int nx = x + dir[i][0];
            int ny = y + dir[i][1];            
            if (nx >= 0 && nx < matrix.length && ny >=0 && ny < matrix[0].length && matrix[nx][ny] > matrix[x][y]){
                if (memory[nx][ny] == 0)
                    memory[nx][ny] = helper(matrix, nx, ny, memory);
                memory[x][y] = Math.max(memory[x][y], memory[nx][ny] + 1);
            }
        }     
        return Math.max(memory[x][y], 1);
    }
}
```

<hr />