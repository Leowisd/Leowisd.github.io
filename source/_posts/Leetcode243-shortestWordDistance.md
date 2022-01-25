---
title: Leetcode243-Shortest Word Distance
categories: leetcode
tags: [Two Pointers, Linkedin]
description: Solution Report of LeetCode Accepted
mathjax: true
date: 2022-01-25 14:28:11
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of strings wordsDict and two different strings that already exist in the array word1 and word2, return the shortest distance between these two words in the list.

## Example

**Example 1:**
```
Input: wordsDict = ["practice", "makes", "perfect", "coding", "makes"], word1 = "coding", word2 = "practice"
Output: 3
```
**Example 2:**
```
Input: wordsDict = ["practice", "makes", "perfect", "coding", "makes"], word1 = "makes", word2 = "coding"
Output: 1
```

**Constraints:**

* 1 <= wordsDict.length <= 3 * 104
* 1 <= wordsDict[i].length <= 10
* wordsDict[i] consists of lowercase English letters.
* word1 and word2 are in wordsDict.
* word1 != word2

## Solution

* Time Complexity: $$O(NM)$$, N is the number of words, M is the length of target word(equal needs O(M) to compare)
* Space Complexity: $$O(1)$$

```java
class Solution {
    public int shortestDistance(String[] wordsDict, String word1, String word2) {
        int p1 = -1;
        int p2 = -1;
        int res = Integer.MAX_VALUE;
        
        for (int i = 0; i < wordsDict.length; i++){
            if (wordsDict[i].equals(word1)){
                p1 = i;
            }
            if (wordsDict[i].equals(word2)){
                p2 = i;
            }
            if (p1 != -1 && p2 != -1){
                res = Math.min(res, Math.abs(p1 - p2));
            }
        }
        
        return res;
    }
}
```

<hr />