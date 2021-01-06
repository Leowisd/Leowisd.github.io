---
title: Leetcode1197-minimumKnightMoves
categories: leetcode
tags: [BFS, Recursion, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-05 21:44:41
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
In an infinite chess board with coordinates from -infinity to +infinity, you have a knight at square [0, 0].

A knight has 8 possible moves it can make, as illustrated below. Each move is two squares in a cardinal direction, then one square in an orthogonal direction.

![](https://assets.leetcode.com/uploads/2018/10/12/knight.png)

Return the minimum number of steps needed to move the knight to the square [x, y].  It is guaranteed the answer exists.
## Example

**Example 1:**
```
Input: x = 2, y = 1
Output: 1
Explanation: [0, 0] → [2, 1]
```
**Example 2:**
```
Input: x = 5, y = 5
Output: 4
Explanation: [0, 0] → [2, 1] → [4, 2] → [3, 4] → [5, 5]
```

**Constraints:**
```
|x| + |y| <= 300
```

## Solution

### Solution 1: BFS

* Time Complexity: $$O()$$
* Space Complexity: $$O()$$

```java
class Solution {
    class Cell{
        int x;
        int y;
        public Cell(int x, int y){
            this.x = x;
            this.y = y;
        }
    }
    public int minKnightMoves(int x, int y) {
        int[][] dir = {{-2, 1},{-1, 2},{1, 2},{2, 1},{2, -1},{1, -2},{-1, -2},{-2, -1}};
        Queue<Cell> q = new LinkedList<>();
        q.offer(new Cell(0, 0));
        HashSet<String> visited = new HashSet<>();
        visited.add("0,0");
        int step = 0;
        x = Math.abs(x);
        y = Math.abs(y);
//      so we can use nx >= 0 and ny >= 0, or need to use nx >= -1, ny >= -1   
        if (x == 1 && y == 1) return 2;
        
        while(!q.isEmpty()){
            int size = q.size();
            for (int j = 0; j < size; j++){
                Cell cur = q.poll();
                if (cur.x == x && cur.y == y)
                    return step;
                for (int[] d : dir){
                    int nx = cur.x + d[0];
                    int ny = cur.y + d[1];
                    if (nx >= 0 && ny >= 0 && !visited.contains(nx + "," + ny)){
                        q.offer(new Cell(nx, ny));
                        visited.add(nx + "," + ny);
                    }
                }
            }
            step++;
        }
        return step;
    }
}
```

### Solution 2: Recursion with memory, faster
```java
class Solution {
    public int minKnightMoves(int x, int y) {
        x = Math.abs(x);
        y = Math.abs(y);
        Map<String, Integer> memo = new HashMap<>();
        return helper(x, y, memo);
    }

    private int helper(int x, int y, Map<String, Integer> memo) {
        String key = x + "," + y;
        if (memo.containsKey(key)) {
            return memo.get(key);
        }
        if (x + y == 0) {
            return 0;
        } else if (x + y == 2) {
            return 2;
        }
        int min = Math.min(helper(Math.abs(x - 1), Math.abs(y - 2), memo), 
                           helper(Math.abs(x - 2), Math.abs(y - 1), memo)) + 1;
        memo.put(key, min);
        return min;
    }
}
```

<hr />