---
title: Leetcode253-meetingRoomsII
categories: leetcode
tags: [Heap, Sort, Greedy, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-06 21:00:50
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

## Example
**Example 1:**
```
Input: [[0, 30],[5, 10],[15, 20]]
Output: 2
```
**Example 2:**
```
Input: [[7,10],[2,4]]
Output: 1
```
## Solution
Method 1, sort, O(NlogN)
```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        if (intervals == null || intervals.length == 0 || intervals[0].length == 0) return 0;
        
        int res = 0;
        int len = intervals.length;
        int[] start = new int[len];
        int[] end = new int[len];
        for (int i = 0; i < len; i++){
            start[i] = intervals[i][0];
            end[i] = intervals[i][1];
        }
        Arrays.sort(start);
        Arrays.sort(end);
        
        int enditr = 0;
        for (int i = 0; i < len; i++){
            if (start[i] < end[enditr]) res++;
            else enditr++;
        }
        return res;
    }
}
```
Method2, Heap, O(NlogN)
```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        if (intervals == null || intervals.length == 0 || intervals[0].length == 0) return 0;
        
        TreeMap<Integer, Integer>map = new TreeMap<>();
        for (int[] it: intervals){
            map.put(it[0], map.getOrDefault(it[0], 0)+1);
            map.put(it[1], map.getOrDefault(it[1], 0)-1);
        }
        
        int res = 0;
        int curRoom = 0;
        for (int time: map.values()){
            curRoom += time;
            res = Math.max(res, curRoom);
        }
        
        return res;
    }
}
```

<hr />