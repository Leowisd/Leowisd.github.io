---
title: Leetcode692-topKFrequentWords
categories: leetcode
tags: [Hash Table, Heap, Amazon, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-08 16:36:11
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

## Example
**Example 1:**
```
Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words.
    Note that "i" comes before "love" due to a lower alphabetical order.
```
**Example 2:**
```
Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
    with the number of occurrence being 4, 3, 2 and 1 respectively.
```
## Solution
O(NlogK)
```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        if (words == null || words.length == 0) return new ArrayList<String>();
        
        HashMap<String, Integer> map = new HashMap<>();
        for (String word: words){
            map.put(word, map.getOrDefault(word, 0)+1);
        }
        
        PriorityQueue<String> pq = new PriorityQueue<>(new Comparator<String>(){
            @Override
            public int compare(String a, String b){
                if (map.get(a) == map.get(b)) return b.compareTo(a);
                else return map.get(a)-map.get(b);
            }
        });
        for (String word: map.keySet()){
            pq.offer(word);
            if (pq.size() > k) pq.poll();
        }
        
        LinkedList<String> res = new LinkedList<>();       
        while(!pq.isEmpty()) res.addFirst(pq.poll());
        
        return res;
    }
}
```

<hr />