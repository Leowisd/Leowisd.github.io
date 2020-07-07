---
title: Leetcode059-spiralMatrixII
categories: leetcode
tags: [Array]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-23 12:28:31
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given a positive integer n, generate a square matrix filled with elements from 1 to $n^2$ in spiral order.

## Example
```
Input: 3
Output:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

## Solution
```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res = new int[n][n];
        for (int i = 0 ; i < n; i++)
            for (int j = 0; j < n; j++)
                res[i][j] = 0;
        int x = 0;
        int y = 0;
        int dir = 1;
        for (int i = 1; i <= n*n; i++){
            res[x][y] = i;
            if (dir == 1){
                if (y == n-1 || res[x][y+1] > 0){
                    x += 1;
                    dir = 2;
                }
                else  y += 1;
            }
            else if (dir == 2){
                if (x == n-1 || res[x+1][y] > 0){
                    y -= 1;
                    dir = 3;
                }
                else x += 1;
            }
            else if (dir == 3){
                if (y == 0 || res[x][y-1] > 0){
                    x -= 1;
                    dir = 4;
                }
                else y -= 1;
            }
            else if (dir == 4){
                if (x == 0 || res[x-1][y] > 0){
                    y += 1;
                    dir = 1;
                }
                else x -= 1;
            }
        }
        return res;
    }
}
```

<hr />