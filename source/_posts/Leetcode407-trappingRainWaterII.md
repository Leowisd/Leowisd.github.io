---
title: Leetcode407-Trapping Rain Water II
categories: leetcode
tags: [Heap, BFS, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-03 16:53:09
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an m x n matrix of positive integers representing the height of each unit cell in a 2D elevation map, compute the volume of water it is able to trap after raining.

## Example
```
Given the following 3x6 height map:
[
  [1,4,3,1,3,2],
  [3,2,1,3,2,4],
  [2,3,3,2,3,1]
]

Return 4.
```
![](https://assets.leetcode.com/uploads/2018/10/13/rainwater_empty.png)
```
The above image represents the elevation map [[1,4,3,1,3,2],[3,2,1,3,2,4],[2,3,3,2,3,1]] before the rain.
```
![](https://assets.leetcode.com/uploads/2018/10/13/rainwater_fill.png)
```
After the rain, water is trapped between the blocks. The total volume of water trapped is 4.
```
**Constraints:**

* 1 <= m, n <= 110
* 0 <= heightMap[i][j] <= 20000

## Solution

* Time Complexity: $$O(M * N)$$
* Space Complexity: $$O(M * N)$$

```java
class Solution {
    class Cell {
        int row;
        int col;
        int height;
        public Cell(int r, int c, int h){
            row = r;
            col = c;
            height = h;
        }
    }
    public int trapRainWater(int[][] heightMap) {
        if (heightMap.length < 2) return 0;
        int m = heightMap.length, n = heightMap[0].length;
        PriorityQueue<Cell> pq = new PriorityQueue<>(new Comparator<Cell>(){
            @Override
            public int compare(Cell c1, Cell c2){
                return c1.height - c2.height; 
            }
        });
        boolean[][] visited = new boolean[m][n];
        
        for (int i = 0; i < m; i++){
            visited[i][0] = true;
            visited[i][n - 1] = true;
            pq.offer(new Cell(i, 0, heightMap[i][0]));
            pq.offer(new Cell(i, n - 1, heightMap[i][n - 1]));
        }
        
        for (int i = 0; i < n; i++){
            visited[0][i] = true;
            visited[m- 1][i] = true;
            pq.offer(new Cell(0, i, heightMap[0][i]));
            pq.offer(new Cell(m - 1, i, heightMap[m - 1][i]));
        }
        
        int res = 0;
        int[] dir = {1, 0, -1, 0, 1};
        while (!pq.isEmpty()){
            Cell cur = pq.poll();
            int row = cur.row, col = cur.col, height = cur.height;
            
            for (int i = 0; i < 4; i++){
                int nx = row + dir[i];
                int ny = col + dir[i + 1];
                if (nx > 0 && nx < m - 1 && ny > 0 && ny < n - 1 && !visited[nx][ny]){
                    visited[nx][ny] = true;
                    res += Math.max(0, height - heightMap[nx][ny]);
                    pq.offer(new Cell(nx, ny, Math.max(height, heightMap[nx][ny])));
                }
            }
        }
        return res;        
    }
}
```

<hr />