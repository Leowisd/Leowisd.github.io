---
title: Leetcode130-surroundedRegions
categories: leetcode
tags: [DFS]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-11-13 23:06:03
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

## Example
```
X X X X
X O O X
X X O X
X O X X
```
After running your function, the board should be:
```
X X X X
X X X X
X X X X
X O X X
```

**Explanation:**

Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.

## Solution
```java
class Solution {
    int[][] direction = new int[][]{{1, 0},{-1, 0},{0, 1},{0, -1}};
    public void solve(char[][] board) {
        if (board == null || board.length == 0) return;
        
        int m = board.length;
        int n = board[0].length;
        for (int i = 0; i < n; i++){
            if (board[0][i] == 'O') dfs(board, 0, i);
            if (board[m - 1][i] == 'O') dfs(board, m-1, i);           
        }
        for (int i = 0; i < m; i++){
            if (board[i][0] == 'O') dfs(board, i, 0);
            if (board[i][n-1] == 'O') dfs(board, i, n-1);           
        }
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++){
                if (board[i][j] == '+') board[i][j] = 'O';
                else board[i][j] = 'X';
            }
    }
    private void dfs(char[][] board, int x, int y){
        board[x][y] = '+';
        for (int i = 0; i < 4; i++){
            int nx = x + direction[i][0];
            int ny = y + direction[i][1];
            if (nx >= 0 && nx < board.length && ny >= 0 && ny < board[0].length && board[nx][ny] == 'O')
                dfs(board, nx, ny);
        }
    }
}
```

<hr />