---
title: Leetcode723-candyCrash
categories: leetcode
tags: [Array, Two Pointers, Bloomberg, Goolge]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 00:13:30
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

This question is about implementing a basic elimination algorithm for Candy Crush.

Given a 2D integer array board representing the grid of candy, different positive integers board[i][j] represent different types of candies. A value of board[i][j] = 0 represents that the cell at position (i, j) is empty. The given board represents the state of the game following the player's move. Now, you need to restore the board to a stable state by crushing candies according to the following rules:

1. If three or more candies of the same type are adjacent vertically or horizontally, "crush" them all at the same time - these positions become empty.
2. After crushing all candies simultaneously, if an empty space on the board has candies on top of itself, then these candies will drop until they hit a candy or bottom at the same time. (No new candies will drop outside the top boundary.)
3. After the above steps, there may exist more candies that can be crushed. If so, you need to repeat the above steps.
4. If there does not exist more candies that can be crushed (ie. the board is stable), then return the current board.

You need to perform the above rules until the board becomes stable, then return the current board.

## Example
```
Input:
board =
[[110,5,112,113,114],[210,211,5,213,214],[310,311,3,313,314],[410,411,412,5,414],[5,1,512,3,3],[610,4,1,613,614],[710,1,2,713,714],[810,1,2,1,1],[1,1,2,2,2],[4,1,4,4,1014]]

Output:
[[0,0,0,0,0],[0,0,0,0,0],[0,0,0,0,0],[110,0,0,0,114],[210,0,0,0,214],[310,0,0,113,314],[410,0,0,213,414],[610,211,112,313,614],[710,311,412,613,714],[810,411,512,713,1014]]
```
Explanation:
![](https://assets.leetcode.com/uploads/2018/10/12/candy_crush_example_2.png)

**Note:**

* The length of board will be in the range [3, 50].
* The length of board[i] will be in the range [3, 50].
* Each board[i][j] will initially start as an integer in the range [1, 200

## Solution
The idea is to traverse the entire matrix again and again to remove crush until no crush can be found.

For each traversal of the matrix, we only check two directions, rightward and downward. There is no need to check upward and leftward because they would have been checked from previous cells.

For each cell, if there are at least three candies of the same type rightward or downward, set them all to its negative value to mark them.

After each traversal, we need to remove all those negative values by setting them to 0, then let the rest drop down to their correct position. A easy way is to iterate through each column, for each column, move positive values to the bottom then set the rest to 0.

```java
class Solution {
    public int[][] candyCrush(int[][] board) {
        if (board == null || board.length == 0 || board[0].length == 0) return board;
        
        int m = board.length;
        int n = board[0].length;
        while (!isStable(board)){
            for (int j = 0; j < n; j++){
                int idx = m - 1;
                for (int i = m - 1; i >= 0; i--){
                    if (board[i][j] > 0) board[idx--][j] = board[i][j];
                }
                for (int i = 0; i <= idx; i++) board[i][j] = 0;
            }
        }
        
        return board;
    }
    
    private boolean isStable(int[][] board){
        boolean flag = true;
        for (int i = 0; i < board.length; i++){
            for (int j = 0; j < board[0].length; j++){
                int cur = Math.abs(board[i][j]);
                if (cur == 0) continue;
                if (j < board[0].length - 2 && cur == Math.abs(board[i][j + 1]) && cur == Math.abs(board[i][j + 2])){
                    flag = false;
                    int temp = j;
                    while(temp < board[0].length && Math.abs(board[i][temp]) == cur){
                        board[i][temp] = -cur;
                        temp++;
                    }
                }
                
                if (i < board.length - 2 && cur == Math.abs(board[i + 1][j]) && cur == Math.abs(board[i + 2][j])){
                    flag = false;
                    int temp = i;
                    while(temp < board.length && Math.abs(board[temp][j]) == cur){
                        board[temp][j] = -cur;
                        temp++;
                    }
                }
            }
        }
        return flag;
    }
}
```

<hr />