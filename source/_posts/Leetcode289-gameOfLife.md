---
title: Leetcode289-gameOfLife
categories: leetcode
tags: [Array, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-06 11:11:43
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

According to the Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

Any live cell with fewer than two live neighbors dies, as if caused by under-population.
Any live cell with two or three live neighbors lives on to the next generation.
Any live cell with more than three live neighbors dies, as if by over-population..
Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.
Write a function to compute the next state (after one update) of the board given its current state. The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously.

## Example
```
Input: 
[
  [0,1,0],
  [0,0,1],
  [1,1,1],
  [0,0,0]
]
Output: 
[
  [0,0,0],
  [1,0,1],
  [0,1,1],
  [0,1,0]
]
```
**Follow up:**

Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?
## Solution
```java
class Solution {
    static int[][] dir = new int[][]{{-1,-1},{-1, 0},{-1, 1},{0, 1},{1, 1},{1, 0},{1, -1},{0, -1}};
    
    public void gameOfLife(int[][] board) {
        if (board == null || board.length == 0 || board[0].length == 0) return;
        int m = board.length;
        int n = board[0].length;
        int[][] newGeneration = new int[m][n];
        
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++){
                int live = countLive(board, i, j, m, n);
                newGeneration[i][j] = board[i][j];
                if (board[i][j] == 1){
                    if (live < 2 || live > 3){
                        newGeneration[i][j] = 0;                       
                    }
                }
                else if (board[i][j] == 0){
                    if (live == 3) newGeneration[i][j] = 1;
                }
            }
        
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++){
                board[i][j] = newGeneration[i][j];
            }
    }
    
    public int countLive(int[][]board, int x, int y, int m, int n){
        int nx = 0;
        int ny = 0;
        int res = 0;
        for (int[] d: dir){
            nx = x + d[0];
            ny = y + d[1];
            if (nx >= 0 && nx < m && ny >= 0 && ny < n){
                if (board[nx][ny] == 1) res++;
            }
        }
        return res;
    }
}
```

Follow 2
```java
class Solution {
// - 00  dead (next) <- dead (current)
// - 01  dead (next) <- live (current)  
// - 10  live (next) <- dead (current)  
// - 11  live (next) <- live (current) 
    public void gameOfLife(int[][] board) {
        if (board == null || board.length == 0) return;
        int m = board.length, n = board[0].length;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int lives = liveNeighbors(board, m, n, i, j);

                // In the beginning, every 2nd bit is 0;
                // So we only need to care about when will the 2nd bit become 1.
                if (board[i][j] == 1 && lives >= 2 && lives <= 3) {  
                    board[i][j] = 3; // Make the 2nd bit 1: 01 ---> 11
                }
                if (board[i][j] == 0 && lives == 3) {
                    board[i][j] = 2; // Make the 2nd bit 1: 00 ---> 10
                }
            }
        }

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] >>= 1;  // Get the 2nd state.
            }
        }
    }

    public int liveNeighbors(int[][] board, int m, int n, int i, int j) {
        int lives = 0;
        for (int x = Math.max(i - 1, 0); x <= Math.min(i + 1, m - 1); x++) {
            for (int y = Math.max(j - 1, 0); y <= Math.min(j + 1, n - 1); y++) {
                lives += board[x][y] & 1;
            }
        }
        lives -= board[i][j] & 1;
        return lives;
    }
}
```

<hr />