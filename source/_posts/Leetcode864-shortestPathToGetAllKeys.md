---
title: Leetcode864-Shortest Path To Get All Keys
categories: leetcode
tags: [BFS, TikTok, Bitwise Operation]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-12-24 00:00:23
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

We are given a 2-dimensional grid. "." is an empty cell, "#" is a wall, "@" is the starting point, ("a", "b", ...) are keys, and ("A", "B", ...) are locks.

We start at the starting point, and one move consists of walking one space in one of the 4 cardinal directions.  We cannot walk outside the grid, or walk into a wall.  If we walk over a key, we pick it up.  We can't walk over a lock unless we have the corresponding key.

For some 1 <= K <= 6, there is exactly one lowercase and one uppercase letter of the first K letters of the English alphabet in the grid.  This means that there is exactly one key for each lock, and one lock for each key; and also that the letters used to represent the keys and locks were chosen in the same order as the English alphabet.

Return the lowest number of moves to acquire all keys.  If it's impossible, return -1.

## Example
**Example 1:**
```
Input: ["@.a.#","###.#","b.A.B"]
Output: 8
```
**Example 2:**
```
Input: ["@..aA","..B#.","....b"]
Output: 6
```
## Solution

* Time Complexity: $$O(m * n * 2^{numOfKey})$$
* Space Complexity: $$O(m * n * 2^{numOfKey})$$

```java
class Solution {
    public int shortestPathAllKeys(String[] grid) {
        if (grid.length == 0 || grid[0].length() == 0) return -1;
        int m = grid.length;
        int n = grid[0].length();
        Queue<Integer> q = new LinkedList<>();
        // Original method 47ms
        HashSet<Integer> visited = new HashSet<>();
        // Optimized method 13ms
        // int[][][] visited = new int[m][n][64];
        int allKeys = 0;
        
        for (int i = 0; i < m; i++){
            for (int j = 0; j < n; j++){
                if (grid[i].charAt(j) == '@'){
                    q.offer((i << 16) | (j << 8));
                    visited.add((i << 16) | (j << 8));
                    // visited[i][j][0] = 1;
                }
                else if (grid[i].charAt(j) >= 'a' && grid[i].charAt(j) <= 'f'){
                    allKeys |= 1 << (grid[i].charAt(j) - 'a');
                }
            }
        }
    
        int[] dir = {-1, 0, 1, 0, -1};
        int res = 0;
        while (!q.isEmpty()){
            int size = q.size();
            for (int i = 0; i < size; i++){
                int cur = q.poll();
                int x = cur >> 16;
                int y = (cur >> 8) & 0xFF;
                int key = cur & 0xFF;
                if (key == allKeys) return res;
                for (int j = 0; j < 4; j++){
                    int nx = x + dir[j];
                    int ny = y + dir[j + 1];
                    if (nx < 0 || ny < 0 || nx >= m || ny >= n){
                        continue;
                    }
                    char ch = grid[nx].charAt(ny);
                    if (ch == '#') continue;
                    if (ch >= 'A' && ch <= 'F' && ((key & (1 << (ch - 'A'))) == 0)) {
                        continue;
                    }
                    int nkey = key;
                    if (ch >= 'a' && ch <= 'f'){
                        nkey |= 1 << (ch - 'a'); 
                    }
                    int ncur = (nx << 16) | (ny << 8) | nkey;
                    if (visited.contains(ncur)){
                        continue;
                    }
                    // if (visited[nx][ny][nkey] == 1){
                    //     continue;
                    // }
                    q.offer(ncur);
                    visited.add(ncur);
                    // visited[nx][ny][nkey] = 1;
                }
            }
            res++;
        }
        return -1;
    }
}
```

<hr />