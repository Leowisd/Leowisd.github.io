---
title: Leetcode348-designTicTacToe
categories: leetcode
tags: [Design, Amazon, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-05 23:03:51
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Design a Tic-tac-toe game that is played between two players on a n x n grid.

You may assume the following rules:

A move is guaranteed to be valid and is placed on an empty block.
Once a winning condition is reached, no more moves is allowed.
A player who succeeds in placing n of their marks in a horizontal, vertical, or diagonal row wins the game.

## Example
```
Example:
Given n = 3, assume that player 1 is "X" and player 2 is "O" in the board.

TicTacToe toe = new TicTacToe(3);

toe.move(0, 0, 1); -> Returns 0 (no one wins)
|X| | |
| | | |    // Player 1 makes a move at (0, 0).
| | | |

toe.move(0, 2, 2); -> Returns 0 (no one wins)
|X| |O|
| | | |    // Player 2 makes a move at (0, 2).
| | | |

toe.move(2, 2, 1); -> Returns 0 (no one wins)
|X| |O|
| | | |    // Player 1 makes a move at (2, 2).
| | |X|

toe.move(1, 1, 2); -> Returns 0 (no one wins)
|X| |O|
| |O| |    // Player 2 makes a move at (1, 1).
| | |X|

toe.move(2, 0, 1); -> Returns 0 (no one wins)
|X| |O|
| |O| |    // Player 1 makes a move at (2, 0).
|X| |X|

toe.move(1, 0, 2); -> Returns 0 (no one wins)
|X| |O|
|O|O| |    // Player 2 makes a move at (1, 0).
|X| |X|

toe.move(2, 1, 1); -> Returns 1 (player 1 wins)
|X| |O|
|O|O| |    // Player 1 makes a move at (2, 1).
|X|X|X|
```

## Solution
$O(1)$ Solution
```java
class TicTacToe {

    int[] rows, cols;
    int d1, d2, n;
    
    public TicTacToe(int n) {
      rows = new int[n];
      cols = new int[n];
      d1 = 0;
      d2 = 0;
      this.n = n;
    }
    
    public int move(int row, int col, int player) {
      int val = (player == 1) ? 1 : -1;
      int target = (player == 1) ? n : -n;
        
      if(row == col) { // diagonal 
        d1 += val;
        if(d1 == target) return player;
      }
        
      if(row + col + 1 == n) { // diagonal 
        d2 += val;
        if(d2 == target) return player;
      }
        
      rows[row] += val;
      cols[col] += val;

      if(rows[row] == target || cols[col] == target) return player;

      return 0;
    }
}
/**
 * Your TicTacToe object will be instantiated and called as such:
 * TicTacToe obj = new TicTacToe(n);
 * int param_1 = obj.move(row,col,player);
 */
```

$O(N)$ Solution
```java
class TicTacToe {
    
    int[][] board;
    int bn;
    /** Initialize your data structure here. */
    public TicTacToe(int n) {
        board = new int[n][n];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                board[i][j] = 0;
        bn = n;
    }
    
    /** Player {player} makes a move at ({row}, {col}).
        @param row The row of the board.
        @param col The column of the board.
        @param player The player, can be either 1 or 2.
        @return The current winning condition, can be either:
                0: No one wins.
                1: Player 1 wins.
                2: Player 2 wins. */
    public int move(int row, int col, int player) {
        board[row][col] = player;
        
        int flag = 0;
        for (int i = 0; i < bn; i++){
            // System.out.println(board[row][i] + " " + player);
            if (board[row][i] != player){
                flag = 1;
                break;
            }
        }
        // System.out.println(flag);
        if (flag == 0) return player;
        
        flag = 0;
        for (int i = 0; i < bn; i++){
            if (board[i][col] != player){
                flag = 1;
                break;
            }
        }
        if (flag == 0) return player;
        
        if (row - col == 0){
            flag = 0;
            int x = 0;
            int y = 0;
            for (int i = 0; i < bn; i++){
                if (board[x][y] != player){
                    flag = 1;
                    break;
                }
                x++;
                y++;
            }
            if (flag == 0) return player;
        }
        if (row + col == bn-1){
            flag = 0;
            int x = 0;
            int y = bn-1;
            for (int i = 0; i < bn; i++){
                if (board[x][y] != player){
                    flag = 1;
                    break;
                }
                x++;
                y--;
            }
            if (flag == 0) return player;
        }
        
        return 0;
        
    }
}
/**
 * Your TicTacToe object will be instantiated and called as such:
 * TicTacToe obj = new TicTacToe(n);
 * int param_1 = obj.move(row,col,player);
 */
``` 

<hr />