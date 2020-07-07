---
title: Leetcode695-maxAreaOFIsland
categories: leetcode
tags: [DFS, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 20:07:36
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty 2D array grid of 0's and 1's, an island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)

## Example
**Example 1:**
```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
Given the above grid, return 6. Note the answer is not 11, because the island must be connected 4-directionally.
```
**Example 2:**
```
[[0,0,0,0,0,0,0,0]]
Given the above grid, return 0.
Note: The length of each dimension in the given grid does not exceed 50.
```
## Solution
```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) return 0;
        int res = 0;
        for (int i = 0; i < grid.length; i++){
            for (int j = 0; j < grid[0].length; j++){
                if (grid[i][j] == 1)
                    res = Math.max(res, helper(grid, i, j));
            }
        }
        return res;
    }
    private int helper(int[][] grid, int x, int y){
        if (x >= 0 && x < grid.length && y >= 0 && y < grid[0].length && grid[x][y] == 1){
            grid[x][y] = 0;
            return 1 + helper(grid, x + 1, y) + helper(grid, x - 1, y) + helper(grid, x, y + 1) + helper(grid, x, y - 1);
        }
        return 0;
    }
}
```

<hr />