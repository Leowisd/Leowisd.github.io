---
title: Leetcode207-courseSchedule
categories: leetcode
tags: [Topological Sort, BFS, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-05 10:32:24
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

## Example
**Example 1:**
```
Input: 2, [[1,0]] 
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
```
**Example 2:**
```
Input: 2, [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
```
## Solution
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (numCourses == 0 || prerequisites == null || prerequisites.length == 0) return true;
        
        Queue<Integer> red = new LinkedList<>();
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) adj.add(new ArrayList<Integer>());
        
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int[] li: prerequisites){
            map.put(li[0], map.getOrDefault(li[0], 0)+1);
            adj.get(li[1]).add(li[0]);
            if (!map.containsKey(li[1])) map.put(li[1], 0);
        }
        
        for (int i = 0; i < numCourses; i++){
            if (map.containsKey(i)){
                if (map.get(i) == 0) red.offer(i);
            }
        }
        
        while(!red.isEmpty()){
            int tmp = red.poll();
            for (int i: adj.get(tmp)){
                if (map.get(i) > 0){
                    map.put(i, map.get(i)-1);
                    if (map.get(i) == 0){
                        red.offer(i);                       
                    }
                }
            }
        }
        
        for (int it: map.keySet()) 
            if (map.get(it) > 0) return false;
        return true;
    }
}
```

<hr />