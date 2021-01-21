---
title: Leetcode051-N-Queens
categories: leetcode
tags: [Backtracking, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-11 15:33:58
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space, respectively.

## Example

**Example 1:**
![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)
```
Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above
```
**Example 2:**
```
Input: n = 1
Output: [["Q"]]
```
## Solution

* Time Complexity: $$O(N!)$$
* Space Complexity: $$O(N)$$

### Solution 1: Basic Backtracking

```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        char[][] board = new char[n][n];
        for(int i = 0; i < n; i++)
            for(int j = 0; j < n; j++)
                board[i][j] = '.';
        List<List<String>> res = new ArrayList<List<String>>();
        dfs(board, 0, res);
        return res;
    }
    
    private void dfs(char[][] board, int colIndex, List<List<String>> res) {
        if(colIndex == board.length) {
            res.add(construct(board));
            return;
        }
        
        for(int i = 0; i < board.length; i++) {
            if(validate(board, i, colIndex)) {
                board[i][colIndex] = 'Q';
                dfs(board, colIndex + 1, res);
                board[i][colIndex] = '.';
            }
        }
    }
    
    private boolean validate(char[][] board, int x, int y) {
        for(int i = 0; i < board.length; i++) {
            for(int j = 0; j < y; j++) {
                if(board[i][j] == 'Q' && (x + j == y + i || x + y == i + j || x == i))
                    return false;
            }
        }
        
        return true;
    }
    
    private List<String> construct(char[][] board) {
        List<String> res = new LinkedList<String>();
        for(int i = 0; i < board.length; i++) {
            String s = new String(board[i]);
            res.add(s);
        }
        return res;
    }
}
```

### Solution 2: with memory
```java
class Solution {
    private void solve(char[][] curr, int idx, int n, List<List<String>> ret, boolean[] col, boolean[] diag1, boolean[] diag2) {
        if (idx == n) {
            List<String> toAdd = new ArrayList<>();
            for (int i = 0; i < n; i ++) {
                toAdd.add(String.valueOf(curr[i]));
            }
            ret.add(toAdd);
            return;
        }

        for (int j = 0; j < n; j ++) {
            if (col[j] || diag1[idx + n - j - 1] || diag2[idx + j]) {
                continue;
            }
            col[j] = true;
            diag1[idx + n - j - 1] = true;
            diag2[idx + j] = true;
            curr[idx][j] = 'Q';
            solve(curr, idx + 1, n, ret, col, diag1, diag2);
            curr[idx][j] = '.';
            col[j] = false;
            diag1[idx + n - j - 1] = false;
            diag2[idx + j] = false;
        }
    }
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ret = new ArrayList<>();
        char[][] curr = new char[n][n];
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < n; j ++) {
                curr[i][j] = '.';
            }
        }
        boolean[] col = new boolean[n];
        boolean[] diag1 = new boolean[2 * n - 1];
        boolean[] diag2 = new boolean[2 * n - 1];
        solve(curr, 0, n, ret, col, diag1, diag2);
        return ret;
    }
}
```

<hr />