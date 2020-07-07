---
title: Leetcode269-alienDictionary
categories: leetcode
tags: [Topological Sort, Amazon, Microsoft, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-04 16:33:39
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

## Example
```
Example 1:

Input:
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]

Output: "wertf"
Example 2:

Input:
[
  "z",
  "x"
]

Output: "zx"
Example 3:

Input:
[
  "z",
  "x",
  "z"
] 

Output: "" 

Explanation: The order is invalid, so return "".
```
**Note:**

1. You may assume all letters are in lowercase.
2. You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
3. If the order is invalid, return an empty string.
4. There may be multiple valid order of letters, return any one of them is fine.

## Solution

The key to this problem is:

* A topological ordering is possible if and only if the graph has no directed cycles

Let's build a graph and perform a DFS. The following states made things easier.

* visited[i] = -1. Not even exist.
* visited[i] = 0. Exist. Non-visited.
* visited[i] = 1. Visiting.
* visited[i] = 2. Visited.

```java
class Solution {
    public String alienOrder(String[] words) {
        int[] visited = new int[26];
        int[][] adj = new int[26][26];
        buildGraph(words, adj, visited);
        StringBuilder res = new StringBuilder();
        for (int i = 0; i < 26; i++){
            if (visited[i] == 0) 
                if (!dfs(adj, visited, res, i)) return "";
        }
        return res.reverse().toString();        
    }
    
    public boolean dfs(int[][] adj, int[] visited, StringBuilder res, int cur){
        visited[cur] = 1;
        for (int i = 0; i < 26; i++){
            if (adj[cur][i] == 1){
                if (visited[i] == 1) return false;
                if (visited[i] == 0)
                    if (!dfs(adj, visited, res, i)) return false;
            }       
        }
        visited[cur] = 2;
        res.append((char)(cur + 'a'));
        return true;
    }
    
    public void buildGraph(String[] words, int[][] adj, int[] visited){
        Arrays.fill(visited, -1);
        
        for (int i = 0; i < words.length; i++){
            for (char ch: words[i].toCharArray()){
                visited[ch - 'a'] = 0;
            }
            if (i > 0){
                String word1 = words[i-1];
                String word2 = words[i];
                int len = Math.min(word1.length(), word2.length());
                for (int j = 0; j < len; j++){
                    char ch1 = word1.charAt(j);
                    char ch2 = word2.charAt(j);
                    if (ch1 != ch2) {
                        adj[ch1 - 'a'][ch2 - 'a'] = 1;
                        break;
                    }
                }
            }
        }
        
    }
}
```

<hr />