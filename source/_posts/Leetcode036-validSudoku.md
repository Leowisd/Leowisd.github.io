---
title: Leetcode036-validSudoku
categories: leetcode
tags: [Hash Table, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-21 16:51:05
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits 1-9 without repetition.
2. Each column must contain the digits 1-9 without repetition.
3. Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)
A partially filled sudoku which is valid.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.


## Example
**Example 1:**
```
Input:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true
```
**Example 2:**
```
Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being 
    modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```
**Note:**

* A Sudoku board (partially filled) could be valid but is not necessarily solvable.
* Only the filled cells need to be validated according to the mentioned rules.
* The given board contain only digits 1-9 and the character '.'.
* The given board size is always 9x9.

## Solution
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        HashSet<String> seen = new HashSet<>();
        for (int i=0; i<9; ++i) {
            for (int j=0; j<9; ++j) {
                char number = board[i][j];
                if (number != '.')
                    if (!seen.add(number + " in row " + i) ||
                        !seen.add(number + " in column " + j) ||
                        !seen.add(number + " in block " + i/3 + "-" + j/3))
                        return false;
            }
        }
        return true;
    }
//     3 hashsets stupid method!!! 
//     public boolean isValidSudoku(char[][] board) {
//         List<HashSet<Integer>> rows = new ArrayList<>();
//         List<HashSet<Integer>> cols = new ArrayList<>();
//         List<HashSet<Integer>> boxes = new ArrayList<>();
        
//         for (int i = 0; i < 9; i++){
//             rows.add(new HashSet<Integer>());
//             cols.add(new HashSet<Integer>());
//             boxes.add(new HashSet<Integer>());
//         }
        
//         for (int i = 0; i < 9; i++){
//             for (int j = 0; j < 9; j++){
//                 if (Character.isDigit(board[i][j])){
//                     int tmp = board[i][j] - '0';
//                     if (rows.get(i).contains(tmp)) return false;
//                     rows.get(i).add(tmp);
//                     if (cols.get(j).contains(tmp)) return false;
//                     cols.get(j).add(tmp);
//                     int b = 0;
//                     if (i <= 2 && j <= 2) b = 0;
//                     else if (i <= 2 && j <= 5) b = 1;
//                     else if (i <= 2 && j <= 8) b = 2;
//                     else if (i <= 5 && j <= 2) b = 3;
//                     else if (i <= 5 && j <= 5) b = 4;
//                     else if (i <= 5 && j <= 8) b = 5;
//                     else if (i <= 8 && j <= 2) b = 6;
//                     else if (i <= 8 && j <= 5) b = 7;
//                     else if (i <= 8 && j <= 8) b = 8;
//                     if (boxes.get(b).contains(tmp)) return false;
//                     boxes.get(b).add(tmp);
//                 }
//             }
//         }
//         return true;
//     }
}
```

<hr />