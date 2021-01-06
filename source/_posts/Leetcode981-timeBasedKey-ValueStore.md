---
title: Leetcode981-timeBasedKey-ValueStore
categories: leetcode
tags: [Hash Table, Divide and Conquer, Google, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-28 11:33:13
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Create a timebased key-value store class TimeMap, that supports two operations.

1. set(string key, string value, int timestamp)
* Stores the key and value, along with the given timestamp.
2. get(string key, int timestamp)
* Returns a value such that set(key, value, timestamp_prev) was called previously, with timestamp_prev <= timestamp.
* If there are multiple such values, it returns the one with the largest timestamp_prev.
* If there are no values, it returns the empty string ("").
## Example
**Example 1:**
```
Input: inputs = ["TimeMap","set","get","get","set","get","get"], inputs = [[],["foo","bar",1],["foo",1],["foo",3],["foo","bar2",4],["foo",4],["foo",5]]
Output: [null,null,"bar","bar",null,"bar2","bar2"]
Explanation:   
TimeMap kv;   
kv.set("foo", "bar", 1); // store the key "foo" and value "bar" along with timestamp = 1   
kv.get("foo", 1);  // output "bar"   
kv.get("foo", 3); // output "bar" since there is no value corresponding to foo at timestamp 3 and timestamp 2, then the only value is at timestamp 1 ie "bar"   
kv.set("foo", "bar2", 4);   
kv.get("foo", 4); // output "bar2"   
kv.get("foo", 5); //output "bar2"   
```
**Example 2:**
```
Input: inputs = ["TimeMap","set","set","get","get","get","get","get"], inputs = [[],["love","high",10],["love","low",20],["love",5],["love",10],["love",15],["love",20],["love",25]]
Output: [null,null,null,"","high","high","low","low"]
```

**Note:**
* All key/value strings are lowercase.
* All key/value strings have length in the range [1, 100]
* The timestamps for all TimeMap.set operations are strictly increasing.
* 1 <= timestamp <= 10^7
* TimeMap.set and TimeMap.get functions will be called a total of 120000 times (combined) per test case.
## Solution
```java
class TimeMap {
    class Node{
        String val;
        int times;
        public Node(String val, int times){
            this.val = val;
            this.times = times;
        }
    }
    
    HashMap<String, List<Node>> map;
    /** Initialize your data structure here. */
    public TimeMap() {
        map = new HashMap<String, List<Node>>();
    }
    
    public void set(String key, String value, int timestamp) {
        if (!map.containsKey(key)) map.put(key, new ArrayList<Node>());
        map.get(key).add(new Node(value, timestamp));
    }
    
    public String get(String key, int timestamp) {
        if (!map.containsKey(key)) return "";
        return binarySearch(map.get(key), timestamp);
    }
    
    private String binarySearch(List<Node> list, int timestamp){
        int left = 0;
        int right = list.size() - 1;
        while(left < right){
            int mid = (left + right) / 2;
            if (list.get(mid).times == timestamp) return list.get(mid).val;
            if (list.get(mid).times < timestamp){
                if (list.get(mid + 1).times > timestamp) return list.get(mid).val;
                left = mid + 1;
            }
            else right = mid - 1;
        }
        return list.get(left).times <= timestamp ? list.get(left).val : "";
    }
}

/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap obj = new TimeMap();
 * obj.set(key,value,timestamp);
 * String param_2 = obj.get(key,timestamp);
 */
```

<hr />