---
title: Leetcode200-numberOfIslands
categories: leetcode
tags: [DFS, BFS, Amazon, Microsoft, Google, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-07 18:45:17
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

## Example
**Example 1:**
```
Input:
11110
11010
11000
00000

Output: 1
```
**Example 2:**
```
Input:
11000
11000
00100
00011

Output: 3
```
## Solution
```java
class Solution {
    
    static int[][] dir = new int[][]{{1,0}, {-1, 0}, {0, 1}, {0, -1}};
    public int numIslands(char[][] grid) {
        int res = 0;
        if (grid == null || grid.length == 0 || grid[0].length == 0) return res;
        
        int m = grid.length;
        int n = grid[0].length;
        for (int i = 0; i < m; i++){
            for (int j = 0; j < n; j++){
                if (grid[i][j] == '1'){
                    res++;
                    clear(grid,i,j,m,n);
                }
            }
        }
        
        return res;
    }
    
    public void clear(char[][] grid, int x, int y, int m, int n){
        if (grid[x][y] == '0') return;
        
        grid[x][y] = '0';
        for (int i = 0; i < 4; i++){
            int nx = x + dir[i][0];
            int ny = y + dir[i][1];
            if (nx >=0 && nx < m && ny >= 0 && ny < n) clear(grid,nx,ny,m,n);
        }
    }
}
```

<hr />