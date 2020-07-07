---
title: Leetcode1057-campusBikes
categories: leetcode
tags: [Greedy, Priority Queue, Sort, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-11-04 15:33:02
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

On a campus represented as a 2D grid, there are N workers and M bikes, with N <= M. Each worker and bike is a 2D coordinate on this grid.

Our goal is to assign a bike to each worker. Among the available bikes and workers, we choose the (worker, bike) pair with the shortest Manhattan distance between each other, and assign the bike to that worker. (If there are multiple (worker, bike) pairs with the same shortest Manhattan distance, we choose the pair with the smallest worker index; if there are multiple ways to do that, we choose the pair with the smallest bike index). We repeat this process until there are no available workers.

The Manhattan distance between two points p1 and p2 is Manhattan(p1, p2) = |p1.x - p2.x| + |p1.y - p2.y|.

Return a vector ans of length N, where ans[i] is the index (0-indexed) of the bike that the i-th worker is assigned to.

## Example
**Example 1:**
![](https://assets.leetcode.com/uploads/2019/03/06/1261_example_1_v2.png)

```
Input: workers = [[0,0],[2,1]], bikes = [[1,2],[3,3]]
Output: [1,0]
Explanation: 
Worker 1 grabs Bike 0 as they are closest (without ties), and Worker 0 is assigned Bike 1. So the output is [1, 0].
```
**Example 2:**
![](https://assets.leetcode.com/uploads/2019/03/06/1261_example_2_v2.png)
```
Input: workers = [[0,0],[1,1],[2,0]], bikes = [[1,0],[2,2],[2,1]]
Output: [0,2,1]
Explanation: 
Worker 0 grabs Bike 0 at first. Worker 1 and Worker 2 share the same distance to Bike 2, thus Worker 1 is assigned to Bike 2, and Worker 2 will take Bike 1. So the output is [0,2,1].
```

**Note:**

1. 0 <= workers[i][j], bikes[i][j] < 1000
2. All worker and bike locations are distinct.
3. 1 <= workers.length <= bikes.length <= 1000

## Solution

Method 1: Priority Queue, O(MNlog(MN)), not the best
```java
class Solution {
    class Pair{
        int worker;
        int bike;
        int dist;
        public Pair(int w, int b, int d){
            worker = w;
            bike = b;
            dist = d;
        } 
    }
    public int[] assignBikes(int[][] workers, int[][] bikes) {
        int[] res = new int[workers.length];
        PriorityQueue<Pair> pq = new PriorityQueue<>(new Comparator<Pair>(){
            @Override
            public int compare(Pair a, Pair b){
                int da = a.dist;
                int db = b.dist;
                if (da != db) return da - db;
                else if (a.worker != b.worker) return a.worker - b.worker;
                else return a.bike - b.bike;
            }
        });
        HashSet<Integer> workerSet = new HashSet<>();
        HashSet<Integer> bikesSet = new HashSet<>();
        
        for (int i = 0; i < workers.length; i++)
            for (int j = 0; j < bikes.length; j++){
                int dist = Math.abs(workers[i][0] - bikes[j][0]) + Math.abs(workers[i][1] - bikes[j][1]);
                pq.offer(new Pair(i, j, dist));
            }
        while(bikesSet.size() < workers.length){
            Pair tmp = pq.poll();
            if (!workerSet.contains(tmp.worker) && !bikesSet.contains(tmp.bike)){
                workerSet.add(tmp.worker);
                bikesSet.add(tmp.bike);
                res[tmp.worker] = tmp.bike;
            }
        }
        return res;
    }
}
```

Method 2: count sorting, O(MN)
```java
class Solution {
        public int[] assignBikes(int[][] workers, int[][] bikes) {
        // Notice that the Manhattan distance is between 0 and 2000, 
        // which means we can sort easily without even using priority queue
        int w = workers.length, b = bikes.length;
        int[] wo = new int[w], bi = new int[b];
        List<int[]>[] dists = new List[2001];
        Arrays.fill(wo, -1);
        Arrays.fill(bi, -1);
        for (int i = 0; i < w; i++) {
            for (int j = 0; j < b; j++) {
                int[] worker = workers[i];
                int[] bike = bikes[j];
                int dist = Math.abs(worker[0] - bike[0]) + Math.abs(worker[1] - bike[1]);
                if (dists[dist] == null) {
                    dists[dist] = new ArrayList<int[]>();
                }
                dists[dist].add(new int[]{i, j});
            }
        }
        int assigned = 0;
        for (int i = 0; i <= 2000 && assigned < w; i++) {
            if (dists[i] == null) continue;
            for (int[] pair : dists[i]) {
                if (wo[pair[0]] == -1 && bi[pair[1]] == -1) {
                    wo[pair[0]] = pair[1];
                    bi[pair[1]] = pair[0];
                    assigned++;
                }
            }
        }
        return wo;
    }
}
```

<hr />