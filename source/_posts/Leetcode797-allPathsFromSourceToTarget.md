---
title: Leetcode797-allPathsFromSourceToTarget
categories: leetcode
tags: [DFS, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-01 23:45:10
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a directed, acyclic graph of N nodes.  Find all possible paths from node 0 to node N-1, and return them in any order.

The graph is given as follows:  the nodes are 0, 1, ..., graph.length - 1.  graph[i] is a list of all nodes j for which the edge (i, j) exists.

## Example
```
Example:
Input: [[1,2], [3], [3], []] 
Output: [[0,1,3],[0,2,3]] 
Explanation: The graph looks like this:
0--->1
|    |
v    v
2--->3
There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```

**Note:**

* The number of nodes in the graph will be in the range [2, 15].
* You can print different paths in any order, but you should keep the order of nodes inside one path.

## Solution
```java
class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        List<List<Integer>> res = new ArrayList<>();
        if (graph == null || graph.length == 0) return res;
        
        helper(graph, res, new ArrayList<Integer>(Arrays.asList(0)), 0);
        
        return res;
    }
    
    private void helper(int[][] graph, List<List<Integer>> res, List<Integer> cur, int pos){
        if (pos == graph.length - 1){
            res.add(new ArrayList<Integer>(cur));
        }
        
        for (int to: graph[pos]){
            cur.add(to);
            helper(graph, res, cur, to);
            cur.remove(cur.size() - 1);
        }
    }
}
```

<hr />