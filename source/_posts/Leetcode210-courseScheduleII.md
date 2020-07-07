---
title: Leetcode210-courseScheduleII
categories: leetcode
tags: [Topological Sort, BFS, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-12 10:33:50
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

## Example
**Example 1:**
```
Input: 2, [[1,0]] 
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished   
             course 0. So the correct course order is [0,1] .
```
**Example 2:**
```
Input: 4, [[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] or [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both     
             courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. 
             So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .
```
**Note:**

1. The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
2. You may assume that there are no duplicate edges in the input prerequisites.

## Solution
```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        if (numCourses == 0) return new int[0];
        int[] res = new int[numCourses];
        Queue<Integer> q = new LinkedList<>();
        HashMap<Integer, List<Integer>> map = new HashMap<>();
        HashMap<Integer, Integer> blue = new HashMap<>();
        for (int i = 0; i < numCourses; i++){
            blue.put(i, 0);
        }
        for (int[] pair: prerequisites){
            if (map.containsKey(pair[1])) map.get(pair[1]).add(pair[0]);
            else {
                map.put(pair[1], new ArrayList<Integer>());
                map.get(pair[1]).add(pair[0]);
            }
            blue.put(pair[0], blue.get(pair[0]) + 1);
        }
        
        for (int node: blue.keySet()){
            if (blue.get(node) == 0){
                q.offer(node);
            }
        }
        
        int index = 0;
        while(!q.isEmpty()){
            int cur = q.poll();
            blue.remove(cur);
            if (map.containsKey(cur)){
                for (int next: map.get(cur)){
                    blue.put(next, blue.get(next)-1);
                    if (blue.get(next) == 0){
                        blue.remove(next);
                        q.offer(next);
                    }
                }
            }
            res[index] = cur;
            index ++;
        }
        if (blue.size() != 0) return new int[0];
        return res;
    }
}
```

<hr />