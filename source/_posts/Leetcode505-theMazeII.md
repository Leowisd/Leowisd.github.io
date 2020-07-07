---
title: Leetcode505-theMazeII
categories: leetcode
tags: [BFS, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-08 16:09:03
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the ball's start position, the destination and the maze, find the shortest distance for the ball to stop at the destination. The distance is defined by the number of empty spaces traveled by the ball from the start position (excluded) to the destination (included). If the ball cannot stop at the destination, return -1.

The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The start and destination coordinates are represented by row and column indexes.

## Example
**Example 1:**
```
Input 1: a maze represented by a 2D array

0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0

Input 2: start coordinate (rowStart, colStart) = (0, 4)
Input 3: destination coordinate (rowDest, colDest) = (4, 4)

Output: 12

Explanation: One shortest way is : left -> down -> left -> down -> right -> down -> right.
             The total distance is 1 + 1 + 3 + 1 + 2 + 2 + 2 = 12.
```
![](https://assets.leetcode.com/uploads/2018/10/12/maze_1_example_1.png)

**Example 2:**
```
Input 1: a maze represented by a 2D array

0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0

Input 2: start coordinate (rowStart, colStart) = (0, 4)
Input 3: destination coordinate (rowDest, colDest) = (3, 2)

Output: -1

Explanation: There is no way for the ball to stop at the destination.
```
![](https://assets.leetcode.com/uploads/2018/10/13/maze_1_example_2.png)

## Solution
```java
class Solution {

    static int[][] dir = new int[][]{{1, 0},{-1, 0},{0, 1},{0, -1}};
    public int shortestDistance(int[][] maze, int[] start, int[] destination) {
        if (maze == null || maze.length == 0 || maze[0].length == 0) return -1;
        if (start == null || start.length == 0 || destination == null || destination.length == 0) return -1;
        
        int m = maze.length, n = maze[0].length;
        int[][] dist = new int[m][n];
        dist[start[0]][start[1]] = 1;
        dfs(start, destination, maze, m, n, dist);
        
        return dist[destination[0]][destination[1]]-1;
    }
    
    private void dfs(int[] s, int[] t, int[][] maze, int m, int n, int[][] dist){
        if (s[1] == t[1] && s[0] == t[0]) return;

        for (int i = 0; i < 4; i++){
            int[] next = new int[]{s[0], s[1]};
            int len = dist[s[0]][s[1]];
            while(next[0] >= 0 && next[0] < m && next[1] >= 0 && next[1] < n && maze[next[0]][next[1]] == 0){
                next[0] = next[0] + dir[i][0];
                next[1] = next[1] + dir[i][1];
                len++;
            }
            next[0] = next[0] - dir[i][0];
            next[1] = next[1] - dir[i][1];
            len--;
            if (dist[next[0]][next[1]] > 0 && dist[next[0]][next[1]] <= len) continue;
            dist[next[0]][next[1]] = len;
            dfs(next, t, maze, m, n, dist);
        }
    }
}
```

<hr />