---
title: Leetcode399-evaluateDivision
categories: leetcode
tags: [Graph, Union Find, Bloomberg, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 20:36:36
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Equations are given in the format A / B = k, where A and B are variables represented as strings, and k is a real number (floating point number). Given some queries, return the answers. If the answer does not exist, return -1.0.

## Example
```
Given a / b = 2.0, b / c = 3.0.
queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ? .
return [6.0, 0.5, -1.0, 1.0, -1.0 ].

The input is: vector<pair<string, string>> equations, vector<double>& values, vector<pair<string, string>> queries , where equations.size() == values.size(), and the values are positive. This represents the equations. Return vector<double>.

According to the example above:

equations = [ ["a", "b"], ["b", "c"] ],
values = [2.0, 3.0],
queries = [ ["a", "c"], ["b", "a"], ["a", "e"], ["a", "a"], ["x", "x"] ]. 
```

The input is always valid. You may assume that evaluating the queries will result in no division by zero and there is no contradiction.

## Solution


Image a/b = k as a link between node a and b, the weight from a to b is k, the reverse link is 1/k. Query is to find a path between two nodes.

What can be improved: Used union find path compression.

```java
class Solution {
    public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
        Map<String, Map<String, Double>> graph = buildGraph(equations, values);
        
        double[] res = new double[queries.size()];
        for (int i = 0; i < res.length; i++){
            res[i] = calculate(graph, queries.get(i).get(0), queries.get(i).get(1), new HashSet<String>());
        }
        return res;
    }
    
//     Calculate the value between s and t
    private double calculate(Map<String, Map<String, Double>> graph, String s, String t, HashSet<String> visited){
        if (!graph.containsKey(s))
            return -1.0;
        
        if (graph.get(s).containsKey(t))
            return graph.get(s).get(t);
        
        visited.add(s);
        for (Map.Entry<String, Double> neighbor: graph.get(s).entrySet()){
            if (!visited.contains(neighbor.getKey())){
                double temp = calculate(graph, neighbor.getKey(), t, visited);
                if (temp != -1)
                    return neighbor.getValue() * temp;    
            }
        }
        
        return -1.0;
    }
    
//     Build a graph
    private Map<String, Map<String, Double>> buildGraph(List<List<String>> equations, double[] values){
        Map<String, Map<String, Double>> graph = new HashMap<>();
        for (int i = 0; i < values.length; i++){
            String a = equations.get(i).get(0);
            String b = equations.get(i).get(1);
            if (!graph.containsKey(a))
                graph.put(a, new HashMap<String, Double>());
            graph.get(a).put(b, values[i]);
            
            if (!graph.containsKey(b))
                graph.put(b, new HashMap<String, Double>());
            graph.get(b).put(a, 1 / values[i]);
        }
        return graph;
    }
}
```

<hr />