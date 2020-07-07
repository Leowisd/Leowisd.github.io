---
title: Leetcode554-brickWall
categories: leetcode
tags: [Hash Table]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-16 22:49:42
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

There is a brick wall in front of you. The wall is rectangular and has several rows of bricks. The bricks have the same height but different width. You want to draw a vertical line from the top to the bottom and cross the least bricks.

The brick wall is represented by a list of rows. Each row is a list of integers representing the width of each brick in this row from left to right.

If your line go through the edge of a brick, then the brick is not considered as crossed. You need to find out how to draw the line to cross the least bricks and return the number of crossed bricks.

**You cannot draw a line just along one of the two vertical edges of the wall, in which case the line will obviously cross no bricks.**

## Example
```
Input: [[1,2,2,1],
        [3,1,2],
        [1,3,2],
        [2,4],
        [3,1,2],
        [1,3,1,1]]

Output: 2

Explanation: 
```
![](https://assets.leetcode.com/uploads/2018/10/12/brick_wall.png)

**Note:**

1. The width sum of bricks in different rows are the same and won't exceed INT_MAX.
2. The number of bricks in each row is in range [1,10,000]. The height of wall is in range [1,10,000]. Total number of bricks of the wall won't exceed 20,000.

## Solution
```java
class Solution {
    public int leastBricks(List<List<Integer>> wall) {
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (List<Integer> row: wall){
            int cur = 0;
            for (int i = 0; i < row.size() - 1; i++){
                cur += row.get(i);
                map.put(cur, map.getOrDefault(cur, 0) + 1);
            }
        }
        
        int temp = 0;
        for (int it: map.keySet()){
            temp = Math.max(temp, map.get(it));
        }
        
        // System.out.println(map);
        return wall.size() - temp;
    }
}
```

<hr />