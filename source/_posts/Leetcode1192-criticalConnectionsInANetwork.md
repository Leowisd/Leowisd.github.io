---
title: Leetcode1192-criticalConnectionsInANetwork
categories: leetcode
tags: [Graph, Tarjan, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-22 22:59:19
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
```
There are n servers numbered from 0 to n-1 connected by undirected server-to-server connections forming a network where connections[i] = [a, b] represents a connection between servers a and b. Any server can reach any other server directly or indirectly through the network.

A critical connection is a connection that, if removed, will make some server unable to reach some other server.

Return all critical connections in the network in any order.
```
## Example
```
Input: n = 4, connections = [[0,1],[1,2],[2,0],[1,3]]
Output: [[1,3]]
Explanation: [[3,1]] is also accepted.
 

Constraints:

1 <= n <= 10^5
n-1 <= connections.length <= 10^5
connections[i][0] != connections[i][1]
There are no repeated connections.
```

## Solution
```java
class Solution {
    int time = 0;
    List<List<Integer>> res = new ArrayList<>();

    public void dfs(int u, List<List<Integer>> graph, int[] disc, int[] low, int[] parent, boolean[] visited){
        visited[u] = true;
        disc[u] = low[u] = ++ time;
        for (int v : graph.get(u)){
            if (!visited[v]){
                parent[v] = u;
                dfs(v, graph, disc, low, parent,visited);
                low[u] = Math.min(low[u], low[v]);
                if (low[v] > disc[u]){
                    List<Integer> tmp = new ArrayList<>();
                    tmp.add(u);
                    tmp.add(v);
                    res.add(tmp);
                }
                    
            }
            else{
                if (v != parent[u]){
                    low[u] = Math.min(low[u], disc[v]);
                }
            }
        }        
    }
    
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++){
            graph.add(new ArrayList<Integer>());
        }
        for (List<Integer> pair : connections){
            int u = pair.get(0);
            int v = pair.get(1);
            graph.get(u).add(v);
            graph.get(v).add(u);
        }
        
        boolean[] visited = new boolean[n];
        int[] disc = new int[n];
        int[] low = new int[n];
        int[] parent = new int[n];
        for (int i = 0 ; i < n; i++){
            visited[i] = false;
            parent[i] = -1;
        }
    
        dfs(0, graph, disc, low, parent,visited);
        return res;
        
    }
}
```

<hr />