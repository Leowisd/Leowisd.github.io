---
title: Leetcode299-bullsAndCows
categories: leetcode
tags: [Hash Table, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 17:51:53
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
You are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.

Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. 

Please note that both secret number and friend's guess may contain duplicate digits.

## Example
**Example 1:**
```
Input: secret = "1807", guess = "7810"

Output: "1A3B"

Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.
```
**Example 2:**
```
Input: secret = "1123", guess = "0111"

Output: "1A1B"

Explanation: The 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow.
```
**Note:** You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.

## Solution
```java
class Solution {
    public String getHint(String secret, String guess) {
        
        int bull = 0, cows = 0;
        char[] sec = secret.toCharArray();
        char[] gue = guess.toCharArray();
        HashMap<Character, Integer> map = new HashMap<>();
        int[] flag = new int[sec.length];
        
        for (int i = 0; i < sec.length; i++){
            if (sec[i] == gue[i]) {
                bull++;
                flag[i] = 0;
            }
            else {
                if (!map.containsKey(sec[i]))
                    map.put(sec[i], 1);
                else map.put(sec[i], map.get(sec[i])+1);
                flag[i] = 1;
            }
            
        }
        
        for (int i = 0; i < sec.length; i++){
            if (flag[i] == 1){
                if (map.containsKey(gue[i])){
                    cows++;
                    map.put(gue[i], map.get(gue[i])-1);
                    if (map.get(gue[i]) == 0)
                        map.remove(gue[i]);
                }
            }
        }
        
        String res = "";
        res = bull + "A" + cows + "B";
        return res;
    }
}
```

<hr />