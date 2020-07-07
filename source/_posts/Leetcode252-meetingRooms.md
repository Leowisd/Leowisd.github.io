---
title: Leetcode252-meetingRooms
categories: leetcode
tags: [Sort, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-28 15:37:00
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

## Example
**Example 1:**
```
Input: [[0,30],[5,10],[15,20]]
Output: false
```
**Example 2:**
```
Input: [[7,10],[2,4]]
Output: true
```

**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

## Solution
```java
class Solution {
    class Pair{
        int start;
        int end;
        public Pair(int start, int end){
            this.start = start;
            this.end = end;
        }
    }
    public boolean canAttendMeetings(int[][] intervals) {
        if (intervals == null || intervals.length == 0 || intervals[0].length == 0) return true;
        Pair[] inter = new Pair[intervals.length];
        for (int i = 0; i < intervals.length; i++){
            inter[i] = new Pair(intervals[i][0], intervals[i][1]);
        }
        Arrays.sort(inter, new Comparator<Pair>(){
            @Override
            public int compare(Pair a, Pair b){
                return a.start - b.start;
            }
        });
        for (int i = 0; i < inter.length - 1; i++){
            if (inter[i].end > inter[i + 1].start)
                return false;
        }
        return true;
    }
}
```

<hr />