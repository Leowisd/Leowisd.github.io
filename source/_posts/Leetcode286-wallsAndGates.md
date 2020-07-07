---
title: Leetcode286-wallsAndGates
categories: leetcode
tags: [BFS, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 20:31:12
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

You are given a m x n 2D grid initialized with these three possible values.

1. -1 - A wall or an obstacle.
2. 0 - A gate.
3. INF - Infinity means an empty room. We use the value 231 - 1 = 2147483647 to represent INF as you may assume that the distance to a gate is less than 2147483647.
Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.

## Example
Given the 2D grid:
```
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
```
After running your function, the 2D grid should be:
```
  3  -1   0   1
  2   2   1  -1
  1  -1   2  -1
  0  -1   3   4
```

## Solution
```java
class Solution {
    private int[][] dir = {{1, 0},{-1, 0},{0, 1},{0, -1}};
    public void wallsAndGates(int[][] rooms) {
        int INF = Integer.MAX_VALUE;
        for (int i = 0; i < rooms.length; i++){
            for (int j = 0; j < rooms[0].length; j++){
                if (rooms[i][j] == 0)
                    helper(rooms, i, j);
            }
        }
    }
    
    private void helper(int[][] rooms, int x, int y){
        int len = 1;
        Queue<int[]> list = new LinkedList<>();
        list.offer(new int[]{x, y});
        while (!list.isEmpty()){
            int size = list.size();
            for (int k = 0; k < size; k++){
                int[] cur = list.poll();
                for (int i = 0; i < dir.length; i++){
                    int nx = cur[0] + dir[i][0];
                    int ny = cur[1] + dir[i][1];
                    if (nx >= 0 && nx < rooms.length && ny >= 0 && ny < rooms[0].length && rooms[nx][ny] > len){
                        rooms[nx][ny] = len;
                        list.offer(new int[]{nx, ny});
                    }
                }    
            }
            len++;
        }
    }
}
```

<hr />