---
title: Leetcode794-validTicTacToeState
categories: leetcode
tags: [Math, Matrix, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-21 15:00:38
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

A Tic-Tac-Toe board is given as a string array board. Return True if and only if it is possible to reach this board position during the course of a valid tic-tac-toe game.

The board is a 3 x 3 array, and consists of characters " ", "X", and "O".  The " " character represents an empty square.

Here are the rules of Tic-Tac-Toe:

* Players take turns placing characters into empty squares (" ").
* The first player always places "X" characters, while the second player always places "O" characters.
* "X" and "O" characters are always placed into empty squares, never filled ones.
* The game ends when there are 3 of the same (non-empty) character filling any row, column, or diagonal.
* The game also ends if all squares are non-empty.
* No more moves can be played if the game is over.

## Example
```
Example 1:
Input: board = ["O  ", "   ", "   "]
Output: false
Explanation: The first player always plays "X".

Example 2:
Input: board = ["XOX", " X ", "   "]
Output: false
Explanation: Players take turns making moves.

Example 3:
Input: board = ["XXX", "   ", "OOO"]
Output: false

Example 4:
Input: board = ["XOX", "O O", "XOX"]
Output: true
```

**Note:**

board is a length-3 array of strings, where each string board[i] has length 3.
Each board[i][j] is a character in the set {" ", "X", "O"}.

## Solution
```java
class Solution {
    public boolean validTicTacToe(String[] board) {
        if (board.length != 3) return false;
        
        int numx = 0;
        int numo = 0;
        int[] rows = new int[3];
        int[] cols = new int[3];
        int d1 = 0;
        int d2 = 0;
        int row = 0;
        for (String s: board){
            if (s.length() != 3) return false;
            int col = 0;
            for (char ch: s.toCharArray()){
                if (ch == 'X'){
                    numx++;
                    rows[row]++;
                    cols[col]++;
                    if (row == col) d1++;
                    if (row + col == 2) d2++;
                }               
                else if (ch == 'O'){
                    numo++;
                    rows[row]--;
                    cols[col]--;
                    if (row == col) d1--;
                    if (row + col == 2) d2--;
                }
                col++;
            }
            row++;
        }
        if (numx < numo) return false;
        if (numx - numo > 1) return false;
        
        int p1 = 0;
        int p2 = 0;
        for (int i = 0; i < 3; i++){
            if (rows[i] == 3) p1++;
            if (cols[i] == 3) p1++;        
            if (rows[i] == -3) p2++;
            if (cols[i] == -3) p2++;
        }
        if (d1 == 3) p1++;
        if (d2 == 3) p1++;
        if (d1 == -3) p2++;
        if (d2 == -3) p2++;

        if (p1 == 2 && p2 == 0 && numx+numo == 9) return true;
        if (p1 > 1 || p2 > 1 || (p1 == 1 && p2 == 1) || (p1 == 1 && numx == numo) || (p2 == 1 && numx > numo)) return false;
        
        return true;
        
    }
}
```

<hr />