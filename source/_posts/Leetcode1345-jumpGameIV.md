---
title: Leetcode1345-Jump Game IV
categories: leetcode
tags: [BFS, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-12 12:25:28
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of integers arr, you are initially positioned at the first index of the array.

In one step you can jump from index i to index:
* i + 1 where: i + 1 < arr.length.
* i - 1 where: i - 1 >= 0.
* j where: arr[i] == arr[j] and i != j.
Return the minimum number of steps to reach the last index of the array.

Notice that you can not jump outside of the array at any time.

## Example

**Example 1:**
```
Input: arr = [100,-23,-23,404,100,23,23,23,3,404]
Output: 3
Explanation: You need three jumps from index 0 --> 4 --> 3 --> 9. Note that index 9 is the last index of the array.
```
**Example 2:**
```
Input: arr = [7]
Output: 0
Explanation: Start index is the last index. You don't need to jump.
```
**Example 3:**
```
Input: arr = [7,6,9,6,9,6,9,7]
Output: 1
Explanation: You can jump directly from index 0 to index 7 which is last index of the array.
```
**Example 4:**
```
Input: arr = [6,1,9]
Output: 2
```
**Example 5:**
```
Input: arr = [11,22,7,7,7,7,7,7,7,22,13]
Output: 3
``` 

**Constraints:**

* 1 <= arr.length <= 5 * 104
* -108 <= arr[i] <= 108

## Solution

### Solution 1: BFS 

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

```java
class Solution {
    public int minJumps(int[] arr) {
        if (arr == null || arr.length == 0) return 0;
        Map<Integer, List<Integer>> map = new HashMap<>();
        for (int i = 0; i < arr.length; i++){
            if (!map.containsKey(arr[i])){
                map.put(arr[i], new ArrayList<>());
            }
            map.get(arr[i]).add(i);
        }
        
        boolean[] visited = new boolean[arr.length];
        Queue<Integer> q = new LinkedList<>();
        q.offer(0);
        visited[0] = true;
        int step = 0;
        while(!q.isEmpty()){
            int size = q.size();
            for (int i = 0; i < size; i++){
                int cur = q.poll();
                if (cur == arr.length - 1) return step;
                List<Integer> next = map.get(arr[cur]);
                next.add(cur - 1);
                next.add(cur + 1);
                for (int ne: next){
                    if (ne >= 0 && ne <= arr.length - 1 && !visited[ne]){
                        visited[ne] = true;
                        q.offer(ne);
                    }
                }
                // to avoid visit element with same value again, for example, 7 7 7 7 2, only add 7 7 7 7for once into the queue.                 
                map.put(arr[cur], new ArrayList<>());
            }
            step++;
        }
        return step;
    }
}
```

### Solution 2: Improved : Bidirectional BFS
```java
class Solution(){
    public int minJumps(int[] arr) {
        if (arr == null || arr.length == 0) return 0;

        Map<Integer, List<Integer>> map = new HashMap<>();
        for (int i = 0; i < arr.length; i++){
            if (!map.containsKey(arr[i])){
                map.put(arr[i], new ArrayList<>());
            }
            map.get(arr[i]).add(i);
        }

        Queue<Integer> q = new LinkedList<>(), q2 = new LinkedList<>();
        boolean[] visited = new boolean[arr.length], visited2 = new boolean[arr.length];
        int step = 0;    

        q.offer(0); 
        visited[0] = true;
        q2.offer(arr.length - 1); 
        visited2[arr.length - 1] = true;

        // Each loop does one BFS step.
        while (q.size() > 0) {
            // Always make the next step with the cheaper search, swap if necessary.
            if (q2.size() < q.size()) {
                Queue<Integer> temp = q;
                q = q2; 
                q2 = temp;

                boolean[] temps = visited;
                visited = visited2; 
                visited2 = temps;
            }

            // Standard BFS step code.
            for (int i = q.size(); i > 0; --i) {
                int cur = q.poll();       
                if (visited2[cur]) return step;   // Check if the two BFS searches meet.

                List<Integer> next = map.get(arr[cur]);
                next.add(cur - 1);
                next.add(cur + 1);
                // Iterate through next possible steps, add unseen ones to the queue.
                for (int ne : next) {                    
                    if (ne >= 0 && ne < arr.length && !visited[ne]) {
                        visited[ne] = true;
                        q.offer(ne);
                    }
                }
                // We remove edges that we go over. We already added all these indices to the queue, there is no need to ever go over them again.
                map.put(arr[cur], new ArrayList<>());   
            }
            step++;
        }
        return step;    
    }
}

```
<hr />