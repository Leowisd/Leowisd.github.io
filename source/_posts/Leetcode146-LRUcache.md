---
title: Leetcode146-LRUcache
categories: leetcode
tags: [Design, Amazon, Microsoft, Bloomberg, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-06 17:06:50
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

The cache is initialized with a positive capacity.

**Follow up:**
Could you do both operations in O(1) time complexity?

## Example
```
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

## Solution

O(1) soluton
```java
class LRUCache {
    class doubleList{
        int key;
        int value;
        doubleList pre;
        doubleList next;
        
        public doubleList(int key, int value, doubleList pre, doubleList next){
            this.key = key;
            this.value = value;
            this.pre = pre;
            this.next = next;
        }
        public doubleList(){
        }
    }
    
    private int capacity;
    private HashMap<Integer, doubleList> map;
    private doubleList head,tail;
    public LRUCache(int capacity){
        this.capacity = capacity;
        map = new HashMap<>();
        head = new doubleList();
        tail = new doubleList();
    }
    
    public int get(int key){
        if (map.containsKey(key)){
            doubleList cur = map.get(key); 

            cur.pre.next = cur.next;
            cur.next.pre = cur.pre;
            
            cur.next = head.next;
            cur.pre = head;
            head.next = cur;
            cur.next.pre = cur;
            
            map.put(key, cur);
            return cur.value;
        }
        return -1;
    }
    
    public void put(int key, int value){
        if (map.containsKey(key)){
            doubleList cur = map.get(key);
            
            cur.pre.next = cur.next;
            cur.next.pre = cur.pre;
            
            cur.next = head.next;
            cur.pre = head;
            head.next = cur;
            cur.next.pre = cur;
            
            cur.value = value;
            map.put(key, cur);
        }
        else{
            if (map.size() == 0){
                doubleList cur = new doubleList(key, value, head, tail);
                head.next = cur;
                tail.pre = cur;
                map.put(key, cur);
            }
            else
            {
                doubleList cur = new doubleList(key, value, head, head.next);
                head.next = cur;
                cur.next.pre = cur;
                map.put(key, cur);
                
                if (map.size() > capacity){
                    map.remove(tail.pre.key);
                    tail.pre.pre.next = tail;
                    tail.pre = tail.pre.pre;
                }
            }
        }
    }
}
/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```
O(N) solution
```java
class LRUCache {
    int capacity;
    HashMap<Integer, Integer> map;
    LinkedList<Integer> keySet;
    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<>();
        keySet = new LinkedList<>();
    }
    
    public int get(int key) {
        if (map.containsKey(key)){
            int value = map.get(key);
            if (keySet.removeFirstOccurrence(key)) keySet.offerFirst(key);
            return value;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        if (map.containsKey(key)){
            map.put(key, value);
            if (keySet.removeFirstOccurrence(key)){
                keySet.offerFirst(key);
            }
        }
        else{
            map.put(key, value);
            keySet.offerFirst(key);
            if (keySet.size() > capacity){
                map.remove(keySet.removeLast());
            }
        }
    }
}
```

<hr />