---
title: Leetcode332-reconstructItinerary
categories: leetcode
tags: [DFS, Graph, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 21:40:18
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a list of airline tickets represented by pairs of departure and arrival airports [from, to], reconstruct the itinerary in order. All of the tickets belong to a man who departs from JFK. Thus, the itinerary must begin with JFK.

**Note:**

1. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].
2. All airports are represented by three capital letters (IATA code).
3. You may assume all tickets form at least one valid itinerary.

## Example
**Example 1:**
```
Input: [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
Output: ["JFK", "MUC", "LHR", "SFO", "SJC"]
```
**Example 2:**
```
Input: [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
Output: ["JFK","ATL","JFK","SFO","ATL","SFO"]
Explanation: Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"].
             But it is larger in lexical order.
```

## Solution
```java
class Solution {
    public List<String> findItinerary(List<List<String>> tickets) {
        HashMap<String, PriorityQueue<String>> map = new HashMap<>();
        for (List<String> pair: tickets){
            String depart = pair.get(0);
            String des = pair.get(1);
            if (!map.containsKey(depart)){
                PriorityQueue<String> pq = new PriorityQueue<>();
                pq.offer(des);
                map.put(depart, pq);
            }
            else{
                map.get(depart).offer(des);
            }
        }
        List<String> res = new LinkedList<>();
        helper(map, res, "JFK");
        return res;
    }
    private void helper(HashMap<String, PriorityQueue<String>> map, List<String> res, String cur){
        while (map.containsKey(cur) && !map.get(cur).isEmpty()){
            helper(map, res, map.get(cur).poll());
        }
        res.add(0, cur);
    }
}
```

<hr />