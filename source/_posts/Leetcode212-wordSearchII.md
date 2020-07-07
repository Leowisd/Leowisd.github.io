---
title: Leetcode212-wordSearchII
categories: leetcode
tags: [DFS, Trie, Hash Table, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-09 12:09:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

## Example
```
Input: 
board = [
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
words = ["oath","pea","eat","rain"]

Output: ["eat","oath"]
```

**Note:**

1. All inputs are consist of lowercase letters a-z.
2. The values of words are distinct.

## Solution

Solution with hashset
```java
class Solution {
    public List<String> findWords(char[][] board, String[] words) {
        if (board == null || board.length == 0 || board[0].length == 0) return new ArrayList<String>();
        
        HashSet<String> set = new HashSet<>();
        HashSet<String> dic = new HashSet<>();
        for (String s: words){
            dic.add(s);
            for (int i = 1; i <= s.length(); i++){
                set.add(s.substring(0,i));
            }
        }
        
        int m = board.length;
        int n = board[0].length;
        HashSet<String> res = new HashSet<>();
        int[][] dir = new int[][]{{1, 0},{-1, 0},{0, 1},{0 ,-1}};
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++){
                String s = "";
                boolean[][] visited = new boolean[m][n];
                visited[i][j]  = true;
                dfs(board, m, n, i, j, dic, set, res, dir, s, visited);
            }
        return new ArrayList<String>(res);
    }
    private void dfs(char[][] board, int m, int n, int x, int y, HashSet<String> dic, HashSet<String> set, HashSet<String> res, int[][] dir, String word, boolean[][] visited){
        word += board[x][y];
        if (dic.contains(word)){
            res.add(word);
        }
        if (!set.contains(word)) return;
        for (int i = 0; i < 4; i++){
            int nx = x + dir[i][0];
            int ny = y + dir[i][1];
            if (nx >= 0 && nx < m && ny >= 0 && ny < n && !visited[nx][ny]){
                visited[nx][ny] = true;
                dfs(board, m, n, nx, ny, dic, set, res, dir, word, visited);
                visited[nx][ny] = false;                
            }
        }
    }
}
```
Solution 2: Trie + DFS
```java
class Solution {    
    public List<String> findWords(char[][] board, String[] words) {
        HashSet<String> res = new HashSet<>();
        TrieNode root = buildTrie(words);
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                dfs (board, i, j, root, res);
            }
        }
        return new ArrayList<String>(res);
    }

    public void dfs(char[][] board, int i, int j, TrieNode p, HashSet<String> res) {
        char c = board[i][j];
        if (c == '#' || p.next[c - 'a'] == null) return;
        p = p.next[c - 'a'];
        if (p.word != null) {   // found one
            res.add(p.word);
            p.word = null;     // de-duplicate
        }

        board[i][j] = '#';
        if (i > 0) dfs(board, i - 1, j ,p, res); 
        if (j > 0) dfs(board, i, j - 1, p, res);
        if (i < board.length - 1) dfs(board, i + 1, j, p, res); 
        if (j < board[0].length - 1) dfs(board, i, j + 1, p, res); 
        board[i][j] = c;
    }

    public TrieNode buildTrie(String[] words) {
        TrieNode root = new TrieNode();
        for (String w : words) {
            TrieNode p = root;
            for (char c : w.toCharArray()) {
                int i = c - 'a';
                if (p.next[i] == null) p.next[i] = new TrieNode();
                p = p.next[i];
            }
        p.word = w;
        }
        return root;
    }

    class TrieNode {
        TrieNode[] next = new TrieNode[26];
        String word;
    }
}
```
<hr />