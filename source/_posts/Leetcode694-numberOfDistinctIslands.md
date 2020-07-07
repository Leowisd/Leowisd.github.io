---
title: Leetcode694-numberOfDistinctIslands
categories: leetcode
tags: [Hash Table, DFS, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-28 15:44:26
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty 2D array grid of 0's and 1's, an island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Count the number of distinct islands. An island is considered to be the same as another if and only if one island can be translated (and not rotated or reflected) to equal the other.

## Example
**Example 1:**
```
11000
11000
00011
00011
```
Given the above grid map, return 1.

**Example 2:**
```
11011
10000
00001
11011
```
Given the above grid map, return 3.

Notice that:
```
11
1
```
and
```
 1
11
```
are considered different island shapes, because we do not consider reflection / rotation.

**Note:** The length of each dimension in the given grid does not exceed 50.

## Solution
```java
class Solution {
    public int numDistinctIslands(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) return 0;
        HashSet<String> set = new HashSet<>();
        for (int i = 0; i < grid.length; i++){
            for (int j = 0; j < grid[0].length; j++){
                if (grid[i][j] != 0){
                    StringBuilder cur= new StringBuilder();
                    helper(grid, i, j, cur, "o");
                    set.add(cur.toString());
                }
            }
        }
        return set.size();
    }
    
    private int[][] direction = new int[][]{{1, 0},{-1, 0},{0, 1},{0, -1}};
    private String[] symbols = new String[]{"d", "u", "r", "l"};
    private void helper(int[][] grid, int x, int y, StringBuilder cur, String dir){
        grid[x][y] = 0;
        cur.append(dir);
        for (int i = 0; i < direction.length; i++){
            int nx = x + direction[i][0];
            int ny = y + direction[i][1];
            if (nx >= 0 && nx < grid.length && ny >= 0 && ny < grid[0].length && grid[nx][ny] == 1){
                helper(grid, nx, ny, cur, symbols[i]);
            }
        }
        cur.append("b");
    }
}
```

<hr />