---
title: Leetcode005-longestPalindrome
tags: [String, Palindrome, Manacher, Amazon, Microsoft, Bloomberg]
mathjax: true
date: 2019-01-22 10:31:43
categories: leetcode
description: Solution Report of LeetCode Acceptted
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

## Example

### Example 1

Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.

### Example 2

Input: "cbbd"

Output: "bb"

## Solution
Most common, $O(N^2)$
```java
class Solution {
    int start;
    int maxLen;    
    public void extend(String s, int a, int b){
        while (a >= 0 && b < s.length() && s.charAt(a) == s.charAt(b)){
            a--;
            b++;
        }
        int len = b - a - 1;
        if (len > maxLen){
            maxLen = len;
            start = a + 1;
        }
    }
    public String longestPalindrome(String s) {
        if (s== null || s.length() == 0) return "";
        if (s.length() < 2) return s;
        for (int i = 0; i < s.length()-1; i++){
            extend(s, i, i);
            extend(s, i, i+1);
        }        
        return s.substring(start, start+maxLen);
    }
}
```

O(N) Manacher
```java
class Solution { 
    public String longestPalindrome(String s) {
        List<Character> a = new ArrayList<>();
        a.add('@');
        a.add('#');
        
        int l = 0; 
        while (l < s.length()){
            a.add(s.charAt(l));
            a.add('#');
            l++;
        }
        a.add('?');
        
        int n = a.size();       
        int maxid = 0;
        int[] p = new int[n];
        int ID = 0;
//     =================    
        int maxPi = 0;
        int index = 0;
//     =================
        for (int i = 1; i < n-1; i++){
            if (maxid > i) p[i] = Math.min(p[2 * ID - i], maxid - i);
            else p[i] = 1;
            
            while(a.get(i+p[i]) == a.get(i-p[i])){
                p[i] ++;
            }
            if (p[i] + i > maxid){
                maxid = p[i] + i;
                ID = i;
            }
//         ==============    
            if (p[i] > maxPi){
                maxPi = p[i];
                index = i;
            }
//         ==============   
        }
//      ==========================   
        int k = index - maxPi + 2;
        String res = "";
        while(maxPi > 1){
            if (a.get(k) != '#'){
                res += a.get(k);
                maxPi --;
            }
            k++;
        }
//      ===========================
        return res;
    }
}
```
DP, $O(N^2)$
```java
class Solution { 
        public void extend(String s, int a, int b){
        if(s.length()==0) return "";
        
        int maxStart = 0;
        int maxEnd = 0;
        
        boolean[][] dp = new boolean[s.length()][s.length()];
        
        //making everything below the diagonal as true
        for(int i=0;i<dp.length;i++)
            for(int j=0;j<i;j++){
                dp[i][j]=true;
            }
        
        int maxLength=0;
        for(int i=s.length()-1;i>=0;i--){
            dp[i][i]=true;   //diagonal as true
            for(int j=i+1;j<s.length();j++){
                if(s.charAt(i)==s.charAt(j) && dp[i+1][j-1]==true){
                    dp[i][j]=true;
                    if(maxLength<j-i){
                        maxLength=j-i;
                        maxStart=i;
                        maxEnd=j;
                    }
                }
            }
        }
        return s.substring(maxStart, maxEnd + 1);
    }
}
```


Using O(n) Manacher algorithm to get the longest palindromic substring

```python
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        a = ['@', '#']
        l = 1
        
        while l <= len(s):
            a.append(s[l-1])
            a.append('#')
            l += 1
        
        a.append('?')
        n = len(a)
        maxid = 0
        p = [1 for i in range(n)]
        ID = 0
        maxPi = 0
        index = 0
  
        for i in range(1, n-2):
            if maxid>i:
                p[i] = min(p[2 * ID - i], maxid-i)
            else:
                p[i] = 1
            
            while a[i+p[i]] == a[i-p[i]]:
                p[i] += 1
            if p[i]+i > maxid:
                maxid = p[i] + i
                ID = i
            if p[i] > maxPi:
                maxPi = p[i]
                index = i

        k = index - maxPi + 2
        result = ''
        while maxPi > 1:
            if a[k] != '#':
                result += a[k]
                maxPi -= 1
            k += 1
        return result
```

<hr />