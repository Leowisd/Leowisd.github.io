---
title: Leetcode727-minimumWindowSubsequence
categories: leetcode
tags: [DP, Sliding Window, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-16 22:46:02
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given strings S and T, find the minimum (contiguous) substring W of S, so that T is a subsequence of W.

If there is no such window in S that covers all characters in T, return the empty string "". If there are multiple such minimum-length windows, return the one with the left-most starting index.

## Example
```
Input: 
S = "abcdebdde", T = "bde"
Output: "bcde"
Explanation: 
"bcde" is the answer because it occurs before "bdde" which has the same length.
"deb" is not a smaller window because the elements of T in the window must occur in order.
```

**Note:**

* All the strings in the input will only contain lowercase letters.
* The length of S will be in the range [1, 20000].
* The length of T will be in the range [1, 100].

## Solution
```java
class Solution {
    public String minWindow(String S, String T) {
        int sidx = 0, tidx = 0;
        int resStart = 0, resEnd = 0;
        int end = 0;
        int resMin = Integer.MAX_VALUE;
        while(sidx < S.length()){
            if (S.charAt(sidx) == T.charAt(tidx)){
                if (tidx == T.length() - 1){
                    end = sidx + 1;
                    tidx--;
                    while(tidx >= 0){
                        sidx--;
                        while (S.charAt(sidx) != T.charAt(tidx)) 
                            sidx--;
                        tidx--;
                    }
                    if(end - sidx < resMin){
                        resMin = end - sidx;
                        resStart = sidx;
                        resEnd = end;
                    }
                }
                tidx++;                
            }
            sidx++;
        }
        
        return S.substring(resStart, resEnd);
    }
}
```

<hr />