---
title: Leetcode347-topKFrequentElements
categories: leetcode
tags: [Hash Table, Heap, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-09-18 22:34:41
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty array of integers, return the k most frequent elements.

## Example

**Example 1:**
```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```
**Example 2:**
```
Input: nums = [1], k = 1
Output: [1]
```
**Note**:
* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

## Solution
```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int x:nums){
            if (map.containsKey(x)){
                map.put(x, map.get(x)+1);
            }
            else map.put(x, 1);
        }

        PriorityQueue<Note> pq = new PriorityQueue<>(k, new Comparator<Note>(){
            @Override
            public int compare(Note a, Note b){
                return a.freq-b.freq;
            }
        });
        for (int x: map.keySet()){
            pq.offer(new Note(x, map.get(x)));
            if (pq.size() > k){
                pq.poll();
            }
        }

        List<Integer> res = new ArrayList<>();
        while (!pq.isEmpty()){
            res.add(pq.poll().val);
        }
        return res;
    }
    
    public class Note{
        int val;
        int freq;
        public Note(int val, int freq){
            this.val = val;
            this.freq = freq;
        }
    }

}
```

<hr />