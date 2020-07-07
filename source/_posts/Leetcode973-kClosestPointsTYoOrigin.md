---
title: Leetcode973-kClosestPointsTYoOrigin
categories: leetcode
tags: [Heap, Divide and Conquer, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-06 15:41:36
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
We have a list of points on the plane.  Find the K closest points to the origin (0, 0).

(Here, the distance between two points on a plane is the Euclidean distance.)

You may return the answer in any order.  The answer is guaranteed to be unique (except for the order that it is in.)

## Example
**Example 1:**
```
Input: points = [[1,3],[-2,2]], K = 1
Output: [[-2,2]]
Explanation: 
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest K = 1 points from the origin, so the answer is just [[-2,2]].
```
**Example 2:**
```
Input: points = [[3,3],[5,-1],[-2,4]], K = 2
Output: [[3,3],[-2,4]]
(The answer [[-2,4],[3,3]] would also be accepted.)
```

## Solution

O(NlogK), Heap
```java
class Solution {
    public int[][] kClosest(int[][] points, int K) {
    
        int[][] res = new int[K][2];
        if (points.length <= K) return points;
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> getDistance(b) - getDistance(a));
        for (int[] point: points){
            pq.offer(point);
            if (pq.size() > K) pq.poll();
        }
        
        for (int i = 0; i < K; i++){
            int[] point = pq.poll();
            res[i][0] = point[0];
            res[i][1] = point[1];
        }
        
        return res;        
    }
    public int getDistance(int[] points) {
        return points[0] * points[0] + points[1] * points[1];
    }
}
```

O(N), Divide and Conquer
```java
class Solution {
    public int[][] kClosest(int[][] points, int K) {
        int len =  points.length, l = 0, r = len - 1;
        while (l <= r) {
            int mid = helper(points, l, r);
            if (mid == K) break;
            if (mid < K) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return Arrays.copyOfRange(points, 0, K);
    }

    private int helper(int[][] A, int l, int r) {
        int[] pivot = A[l];
        while (l < r) {
            while (l < r && compare(A[r], pivot) >= 0) r--;
            A[l] = A[r];
            while (l < r && compare(A[l], pivot) <= 0) l++;
            A[r] = A[l];
        }
        A[l] = pivot;
        return l;
    }

    private int compare(int[] p1, int[] p2) {
        return p1[0] * p1[0] + p1[1] * p1[1] - p2[0] * p2[0] - p2[1] * p2[1];
    }
}
 
```

<hr />