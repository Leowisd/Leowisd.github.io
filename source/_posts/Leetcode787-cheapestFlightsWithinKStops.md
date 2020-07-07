---
title: Leetcode787-cheapestFlightsWithinKStops
categories: leetcode
tags: [Heap, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-29 23:47:50
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

There are n cities connected by m flights. Each flight starts from city u and arrives at v with a price w.

Now given all the cities and flights, together with starting city src and the destination dst, your task is to find the cheapest price from src to dst with up to k stops. If there is no such route, output -1.

## Example
**Example 1:**
```
Input: 
n = 3, edges = [[0,1,100],[1,2,100],[0,2,500]]
src = 0, dst = 2, k = 1
Output: 200
Explanation: 
The graph looks like this:
```
![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/02/16/995.png)
```
The cheapest price from city 0 to city 2 with at most 1 stop costs 200, as marked red in the picture.
```
**Example 2:**
```
Input: 
n = 3, edges = [[0,1,100],[1,2,100],[0,2,500]]
src = 0, dst = 2, k = 0
Output: 500
Explanation: 
The graph looks like this:
```
![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/02/16/995.png)
```
The cheapest price from city 0 to city 2 with at most 0 stop costs 500, as marked blue in the picture.
```

**Note:**

* The number of nodes n will be in range [1, 100], with nodes labeled from 0 to n - 1.
* The size of flights will be in range [0, n * (n - 1) / 2].
* The format of each flight will be (src, dst, price).
* The price of each flight will be in the range [1, 10000].
* k is in the range of [0, n - 1].
* There will not be any duplicated flights or self cycles.

## Solution
```java
// It happen to be the same idea of Dijkstra's algorithm, but we need to keep the path.
// It could not need visited, here "k" limited the time we can visit a single node that it wont go into an infinite loop. (and the n in range[1,100]), but will be slower.
class Solution {
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int K) {
        Map<Integer, Map<Integer, Integer>> map = new HashMap<>();
//         construct map
        for (int[] flight: flights){
            if (!map.containsKey(flight[0]))
                map.put(flight[0], new HashMap<>());
            map.get(flight[0]).put(flight[1], flight[2]);
        }
        
//      used priorityqueue to store distances
        PriorityQueue<int[]> pq = new PriorityQueue<>(new Comparator<int[]>(){
            @Override
            public int compare(int[] a, int b[]){
                return a[0] - b[0];
            }
        });
        pq.offer(new int[]{0, src, K + 1});

//         Visited set
        HashSet<Integer> set = new HashSet<>();

        while(!pq.isEmpty()){
            int[] first = pq.poll();
            int price = first[0];
            int city = first[1];
            int stops = first[2];
            set.add(city);
            
            if (city == dst)
                return price;
            if (stops > 0){
                Map<Integer, Integer> adj = map.getOrDefault(city, new HashMap<>());
                for (int a: adj.keySet()){
                    if (!set.contains(a))
                        pq.add(new int[]{adj.get(a) + price, a, stops - 1});
                }
                
            }
        }
        
        return -1;
    }
}
```

<hr />