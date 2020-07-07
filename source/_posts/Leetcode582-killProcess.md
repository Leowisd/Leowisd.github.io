---
title: Leetcode582-killProcess
categories: leetcode
tags: [Tree, Queue, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-02 11:50:56
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given n processes, each process has a unique PID (process id) and its PPID (parent process id).

Each process only has one parent process, but may have one or more children processes. This is just like a tree structure. Only one process has PPID that is 0, which means this process has no parent process. All the PIDs will be distinct positive integers.

We use two list of integers to represent a list of processes, where the first list contains PID for each process and the second list contains the corresponding PPID.

Now given the two lists, and a PID representing a process you want to kill, return a list of PIDs of processes that will be killed in the end. You should assume that when a process is killed, all its children processes will be killed. No order is required for the final answer.

## Example
```
Input: 
pid =  [1, 3, 10, 5]
ppid = [3, 0, 5, 3]
kill = 5
Output: [5,10]
Explanation: 
           3
         /   \
        1     5
             /
            10
Kill 5 will also kill 10.
```

**Note:**
The given kill id is guaranteed to be one of the given PIDs.
n >= 1.

## Solution
```java
class Solution {
    public List<Integer> killProcess(List<Integer> pid, List<Integer> ppid, int kill) {
        List<Integer> res = new ArrayList<>();
        if (pid == null || pid.size() == 0) return res;
        
        HashMap<Integer, List<Integer>> map = new HashMap<>();
        for (int i = 0; i < ppid.size(); i++){
            int parent = ppid.get(i);
            int child = pid.get(i);
            if (!map.containsKey(parent)){
                map.put(parent, new ArrayList<Integer>());
            }
            map.get(parent).add(child);
        }
        
        Queue<Integer> q = new LinkedList<>();
        q.offer(kill);
        while(!q.isEmpty()){
            int cur = q.poll();
            res.add(cur);
            if (map.containsKey(cur))
                for (int child: map.get(cur))
                    q.offer(child);
        }
        
        return res;
    }
}
```

<hr />