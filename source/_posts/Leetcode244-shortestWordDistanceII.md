---
title: Leetcode244-Shortest Word Distance II
categories: leetcode
tags: [Two Pointers, Hash Table, Linkedin]
description: Solution Report of LeetCode Accepted
mathjax: true
date: 2022-01-25 14:18:13
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Design a data structure that will be initialized with a string array, and then it should answer queries of the shortest distance between two different strings from the array.

Implement the WordDistance class:

WordDistance(String[] wordsDict) initializes the object with the strings array wordsDict.
int shortest(String word1, String word2) returns the shortest distance between word1 and word2 in the array wordsDict.

## Example

```
Input
["WordDistance", "shortest", "shortest"]
[[["practice", "makes", "perfect", "coding", "makes"]], ["coding", "practice"], ["makes", "coding"]]
Output
[null, 3, 1]

Explanation
WordDistance wordDistance = new WordDistance(["practice", "makes", "perfect", "coding", "makes"]);
wordDistance.shortest("coding", "practice"); // return 3
wordDistance.shortest("makes", "coding");    // return 1
```

**Constraints:**

* 1 <= wordsDict.length <= 3 * 104
* 1 <= wordsDict[i].length <= 10
* wordsDict[i] consists of lowercase English letters.
* word1 and word2 are in wordsDict.
* word1 != word2
* At most 5000 calls will be made to shortest.

## Solution

Store index of each words of words dictionary in a map, then using two pointers to compare sorted index array.

if w[i]<w[j], i plus 1, else j plus 1.

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(N)$$

```java
class WordDistance {
    HashMap<String, List<Integer>> map;
    public WordDistance(String[] wordsDict) {
        map = new HashMap<>();
        for (int i = 0; i < wordsDict.length; i++){
            List<Integer> list = map.getOrDefault(wordsDict[i], new ArrayList<>());
            list.add(i);
            map.put(wordsDict[i], list);
        }
    }
    
    public int shortest(String word1, String word2) {
        List<Integer> l1 = map.get(word1);
        List<Integer> l2 = map.get(word2);
        int res = Integer.MAX_VALUE;
        int i = 0, j = 0;
        while(i < l1.size() && j < l2.size()){
            res = Math.min(res, Math.abs(l1.get(i) - l2.get(j)));
            if (l1.get(i) < l2.get(j)){
                i++;
            }
            else{
                j++;
            }
        }
        
        return res;
    }
}

/**
 * Your WordDistance object will be instantiated and called as such:
 * WordDistance obj = new WordDistance(wordsDict);
 * int param_1 = obj.shortest(word1,word2);
 */
```

<hr />