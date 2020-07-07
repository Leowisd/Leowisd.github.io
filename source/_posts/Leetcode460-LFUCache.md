---
title: Leetcode460-LFUCache
categories: leetcode
tags: [Design, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-07 11:36:05
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Design and implement a data structure for Least Frequently Used (LFU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reaches its capacity, it should invalidate the least frequently used item before inserting a new item. For the purpose of this problem, when there is a tie (i.e., two or more keys that have the same frequency), the least recently used key would be evicted.

Note that the number of times an item is used is the number of calls to the get and put functions for that item since it was inserted. This number is set to zero when the item is removed.

**Follow up:**
Could you do both operations in O(1) time complexity?

## Example
```
LFUCache cache = new LFUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.get(3);       // returns 3.
cache.put(4, 4);    // evicts key 1.
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

## Solution
```java
class LFUCache {
    
    HashMap<Integer, Integer> vals;
    HashMap<Integer, Integer> counts;
    HashMap<Integer, LinkedHashSet<Integer>> time;
    int min;
    int cap;
    public LFUCache(int capacity) {
        min = -1;
        cap = capacity;
        vals = new HashMap<>();
        counts = new HashMap<>();
        time = new HashMap<>();
        time.put(1, new LinkedHashSet<>());
    }
    
    public int get(int key) {
        if (!vals.containsKey(key)) return -1;
        
        int count = counts.get(key);
        counts.put(key, count+1);
        time.get(count).remove(key);
        if (min == count && time.get(min).size() == 0) min ++;
        if (!time.containsKey(count+1)) time.put(count + 1, new LinkedHashSet<Integer>());
        time.get(count + 1).add(key);
        
        return vals.get(key);
    }
    
    public void put(int key, int value) {
        if (cap <= 0) return;
        if (vals.containsKey(key)){
            vals.put(key, value);
            get(key);
        }
        else {
            if (vals.size() >= cap){
                int evict = time.get(min).iterator().next();
                time.get(min).remove(evict);
                vals.remove(evict);
                counts.remove(evict);
            }
            vals.put(key, value);
            min = 1;
            counts.put(key, min);
            time.get(1).add(key);
        }
    }
}

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache obj = new LFUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

<hr />