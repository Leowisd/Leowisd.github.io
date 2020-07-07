---
title: Leetcode1254-numberOfClosedIslands
categories: leetcode
tags: [DFS]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-10 21:51:10
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a 2D grid consists of 0s (land) and 1s (water).  An island is a maximal 4-directionally connected group of 0s and a closed island is an island totally (all left, top, right, bottom) surrounded by 1s.

Return the number of closed islands.

## Example
**Example 1:**
```
Input: grid = [[1,1,1,1,1,1,1,0],[1,0,0,0,0,1,1,0],[1,0,1,0,1,1,1,0],[1,0,0,0,0,1,0,1],[1,1,1,1,1,1,1,0]]
Output: 2
Explanation: 
Islands in gray are closed because they are completely surrounded by water (group of 1s).
```

**Example 2:**
```
Input: grid = [[0,0,1,0,0],[0,1,0,1,0],[0,1,1,1,0]]
Output: 1
```

**Example 3:**
```
Input: grid = [[1,1,1,1,1,1,1],
               [1,0,0,0,0,0,1],
               [1,0,1,1,1,0,1],
               [1,0,1,0,1,0,1],
               [1,0,1,1,1,0,1],
               [1,0,0,0,0,0,1],
               [1,1,1,1,1,1,1]]
Output: 2
```

## Solution
```java
class Solution {
    int[][] direction = {{1,0},{-1,0},{0,1},{0,-1}};
    public int closedIsland(int[][] grid) {
        if (grid.length == 0 || grid[0].length == 0) return 0;
        for (int i = 0; i < grid.length; i++){
            if (grid[i][0] == 0) helper(grid, i, 0);
            if (grid[i][grid[0].length - 1] == 0) helper(grid, i, grid[0].length - 1);
        }
        for (int i = 0; i < grid[0].length; i++){
            if (grid[0][i] == 0) helper(grid, 0, i);
            if (grid[grid.length - 1][i] == 0) helper(grid, grid.length - 1, i);
        }
        int res = 0;
        for (int i = 0; i < grid.length; i++){
            for (int j = 0; j < grid[0].length; j++){
                if (grid[i][j] == 0){
                    res ++;
                    helper(grid, i, j);
                }
            }
        }
        return res;
    }
    private void helper(int[][] grid, int x, int y){
        if (grid[x][y] == 0) grid[x][y] = 1;
        for (int i = 0; i < direction.length; i++){
            int nx = x + direction[i][0];
            int ny = y + direction[i][1];
            if (nx >= 0 && nx < grid.length && ny >= 0 && ny < grid[0].length && grid[nx][ny] == 0){
                helper(grid, nx, ny);
            }
        }
    }
}
```

<hr />