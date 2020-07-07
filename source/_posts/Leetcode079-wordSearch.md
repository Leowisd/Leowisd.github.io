---
title: Leetcode079-wordSearch
categories: leetcode
tags: [DFS, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-13 11:22:01
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

## Example
```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

## Solution
```java
class Solution {
    static private int[][] dirt = new int[][]{{1, 0},{-1, 0},{0, 1},{0, -1}};
    public boolean exist(char[][] board, String word) {
        if (board == null || board.length == 0 || board[0].length == 0) return false;
        if (word == null || word.length() == 0) return true;
        char[] w = word.toCharArray();
        boolean[][] visited = new boolean[board.length][board[0].length];
        for (int i = 0; i < board.length; i++)
            for (int j = 0; j < board[0].length; j++)
                if (dfs(board, i, j, w, 0, visited)) return true;                            
        return false;
    }
    public boolean dfs(char[][] board, int x, int y, char[] w, int cur, boolean[][] visited){
        if (board[x][y] != w[cur]) return false;
        if (cur == w.length - 1) return true;
        visited[x][y] = true;
        for (int i = 0; i < 4; i++){
            int nx = x + dirt[i][0];
            int ny = y + dirt[i][1];
            if (nx >= 0 && nx < board.length && ny >=0 && ny < board[0].length && !visited[nx][ny]){
                if (dfs(board, nx, ny, w, cur + 1, visited)) return true;
            }
        }
        visited[x][y] = false;
        return false;
    }
}
```

<hr />