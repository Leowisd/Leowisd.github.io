---
title: Leetcode417-pacificAtlanticWaterFlow
categories: leetcode
tags: [DFS, BFS, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 16:39:41
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an m x n matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions (up, down, left, or right) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

**Note:**

1. The order of returned grid coordinates does not matter.
2. Both m and n are less than 150.

## Example
```
Given the following 5x5 matrix:

  Pacific ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * Atlantic

Return:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).
```

## Solution
```java
// Used two arrays to record if each cell can reach pacific or atlantic.
// Start from four sides to do DFS.

class Solution {
    public List<List<Integer>> pacificAtlantic(int[][] matrix) {
        List<List<Integer>> res = new ArrayList<>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return res;
        
        int m = matrix.length;
        int n = matrix[0].length;
        boolean[][] pacific = new boolean[m][n];
        boolean[][] altantic = new boolean[m][n];
        for (int i = 0; i < m; i++){
            helper(matrix, pacific, i, 0);
            helper(matrix, altantic, i, n - 1);
        }
        for (int i = 0; i < n; i++){
            helper(matrix, pacific, 0, i);
            helper(matrix, altantic, m - 1, i);
        }
        
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++){
                if (pacific[i][j] && altantic[i][j])
                    res.add(new ArrayList<Integer>(Arrays.asList(i, j)));
            }
        
        return res;
    }
    
    private int[][] dir = new int[][]{{-1, 0},{1, 0},{0, -1},{0, 1}};
    private void helper(int[][] matrix, boolean[][] reachable, int x, int y){
        reachable[x][y] = true;
        for (int[] d: dir){
            int nx = x + d[0];
            int ny = y + d[1];
            if (nx >=0 && nx < matrix.length && ny >= 0 && ny < matrix[0].length && !reachable[nx][ny] && matrix[nx][ny] >= matrix[x][y])
                helper(matrix, reachable, nx, ny);
        }
    }
}
```

<hr />