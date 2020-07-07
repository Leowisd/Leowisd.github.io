---
title: Leetcode980-uniquePathsIII
categories: leetcode
tags: [DFS, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-14 10:42:03
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

On a 2-dimensional grid, there are 4 types of squares:

* 1 represents the starting square.  There is exactly one starting square.
* 2 represents the ending square.  There is exactly one ending square.
* 0 represents empty squares we can walk over.
* -1 represents obstacles that we cannot walk over.

Return the number of 4-directional walks from the starting square to the ending square, that **walk over every non-obstacle square exactly once**.

## Example
**Example 1:**
```
Input: [[1,0,0,0],[0,0,0,0],[0,0,2,-1]]
Output: 2
Explanation: We have the following two paths: 
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2)
2. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2)
```
**Example 2:**
```
Input: [[1,0,0,0],[0,0,0,0],[0,0,0,2]]
Output: 4
Explanation: We have the following four paths: 
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2),(2,3)
2. (0,0),(0,1),(1,1),(1,0),(2,0),(2,1),(2,2),(1,2),(0,2),(0,3),(1,3),(2,3)
3. (0,0),(1,0),(2,0),(2,1),(2,2),(1,2),(1,1),(0,1),(0,2),(0,3),(1,3),(2,3)
4. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2),(2,3)
```
**Example 3:**
```
Input: [[0,1],[2,0]]
Output: 0
Explanation: 
There is no path that walks over every empty square exactly once.
Note that the starting and ending square can be anywhere in the grid.
```
## Solution
```java
class Solution {
    private int res = 0;
    private int[][] dir = new int[][]{{1, 0},{-1, 0},{0, 1},{0, -1}};
    public int uniquePathsIII(int[][] grid) {
        int numOb = 0;
        int[] start = new int[2];
        int[] end = new int[2];
        for (int i = 0; i < grid.length; i++)
            for (int j = 0; j < grid[0].length; j++){
                if (grid[i][j] == -1) numOb++;
                if (grid[i][j] == 1){
                    start[0] = i;
                    start[1] = j;
                }                
            }
        
        boolean[][] visited = new boolean[grid.length][grid[0].length];
        dfs(grid, start[0], start[1], visited, numOb, 1);
        
        return res;
    }
    
    private void dfs(int[][] grid, int x, int y, boolean[][] visited, int numOb, int len){
        if (grid[x][y] == 2){
            if (len == grid.length * grid[0].length - numOb)
                res ++;
            return;
        }
        visited[x][y] = true;
        for (int i = 0; i < 4; i++){
            int nx = x + dir[i][0];
            int ny = y + dir[i][1];
            if (nx >= 0 && nx < grid.length && ny >= 0 && ny < grid[0].length && !visited[nx][ny] && grid[nx][ny] != -1){
                dfs(grid, nx, ny, visited, numOb, len + 1);
            }
        }
        visited[x][y] = false;
    }
}
```

<hr />