---
title: Leetcode937-reorderDataInLogFiles
categories: leetcode
tags: [String, Comparator, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-07 21:49:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

You have an array of logs.  Each log is a space delimited string of words.

For each log, the first word in each log is an alphanumeric identifier.  Then, either:

Each word after the identifier will consist only of lowercase letters, or;
Each word after the identifier will consist only of digits.
We will call these two varieties of logs letter-logs and digit-logs.  It is guaranteed that each log has at least one word after its identifier.

Reorder the logs so that all of the letter-logs come before any digit-log.  The letter-logs are ordered lexicographically ignoring identifier, with the identifier used in case of ties.  The digit-logs should be put in their original order.

Return the final order of the logs.

## Example
```
Input: logs = ["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]
Output: ["let1 art can","let3 art zero","let2 own kit dig","dig1 8 1 5 1","dig2 3 6"]
```

**Constraints**:

1. 0 <= logs.length <= 100
2. 3 <= logs[i].length <= 100
3. logs[i] is guaranteed to have an identifier, and a word after the identifier.

## Solution
```java
class Solution {
    public String[] reorderLogFiles(String[] logs) {
        String[] res = new String[logs.length];
        if (logs == null || logs.length == 0) return res;
        
        Arrays.sort(logs, new Comparator<String>(){
            @Override
            public int compare(String a, String b){
                int index1 = a.indexOf(' ');
                int index2 = b.indexOf(' ');
                char ch1 = a.charAt(index1 + 1);
                char ch2 = b.charAt(index2 + 1);
                
                if (ch1 <= '9'){
                    if (ch2 <= '9') return 0;
                    else return 1;
                }
                if (ch2 <= '9') return -1;
                
                int tmp = a.substring(index1+1, a.length()).compareTo(b.substring(index2+1, b.length()));
                if (tmp == 0) tmp = a.substring(0, index1).compareTo(b.substring(0, index2));
                return tmp;
            }
        });
        return logs;
    }
}
```

<hr />