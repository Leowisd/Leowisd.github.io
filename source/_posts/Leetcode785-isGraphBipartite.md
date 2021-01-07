---
title: Leetcode785-Is Graph Bipartite?
categories: leetcode
tags: [BFS, DFS, Bipartite, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-07 01:30:46
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an undirected graph, return true if and only if it is bipartite.

Recall that a graph is bipartite if we can split its set of nodes into two independent subsets A and B, such that every edge in the graph has one node in A and another node in B.

The graph is given in the following form: graph[i] is a list of indexes j for which the edge between nodes i and j exists.  Each node is an integer between 0 and graph.length - 1.  There are no self edges or parallel edges: graph[i] does not contain i, and it doesn't contain any element twice.

## Example

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/21/bi1.jpg)

```
Input: graph = [[1,3],[0,2],[1,3],[0,2]]
Output: true
Explanation: We can divide the vertices into two groups: {0, 2} and {1, 3}.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/21/bi2.jpg)

```
Input: graph = [[1,2,3],[0,2],[0,1,3],[0,2]]
Output: false
Explanation: We cannot find a way to divide the set of nodes into two independent subsets.
```
 

**Constraints:**

* 1 <= graph.length <= 100
* 0 <= graph[i].length < 100
* 0 <= graph[i][j] <= graph.length - 1
* graph[i][j] != i
* All the values of graph[i] are unique.
* The graph is guaranteed to be undirected. 

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

### Solution 1: DFS

```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        int[] colors = new int[n];  

        for (int i = 0; i < n; i++){
            if (colors[i] == 0 && !valid(graph, colors, 1, i)){
                return false;
            }
        }      

        return true;
    }
    
    private boolean valid(int[][] graph, int[] colors, int color, int node){
        if (colors[node] != 0){
            return colors[node] == color;
        }
        colors[node] = color;
        for (int next : graph[node]){
            if (!valid(graph, colors, -color, next)){
                return false;
            }
        }
        return true;
    }
}
```

### Solution 2: BFS
```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        int[] colors = new int[n];
        
        for (int i = 0; i < n; i++){
            if (colors[i] != 0) continue;
            Queue<Integer> q = new LinkedList<>();
            q.offer(i);
            colors[i] = 1;
            
            while(!q.isEmpty()){
                int cur = q.poll();
                for (int next: graph[cur]){
                    if (colors[next] == 0){
                        colors[next] = -colors[cur];
                        q.offer(next);
                    }
                    else if (colors[next] == colors[cur]){
                        return false;
                    }
                }
            }
        }
        
        return true;
    }
}
```

<hr />