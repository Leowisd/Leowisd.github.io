---
title: Leetcode093-restoreIPAddresses
categories: leetcode
tags: [String, Backtracking, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-22 16:40:02
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

## Example
```
Input: "25525511135"
Output: ["255.255.11.135", "255.255.111.35"]
```

## Solution
```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> res = new ArrayList<>();
        dfs(res, 0, s, "");
        return res;
    }
    
    private void dfs(List<String> res, int index, String s, String cur){
        if (index == 3){
            if (s.length() > 1 && s.charAt(0) == '0') return; 
            if (Double.parseDouble(s) > 255) return;
            res.add(cur+s);
            return;
        }
        for (int i = 1; i < Math.min(s.length(), 4); i++){
            String tmp = s.substring(0, i);
            if (tmp.length() > 1 && tmp.charAt(0) == '0') continue;
            if (Double.parseDouble(tmp) > 255) continue;
            cur = cur + tmp + ".";
            dfs(res, index + 1, s.substring(i), cur);
            cur = cur.substring(0, cur.length()-tmp.length()-1);
        }
    }
}
```

<hr />