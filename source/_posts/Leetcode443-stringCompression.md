---
title: Leetcode443-stringCompression
categories: leetcode
tags: [String, Array, Microsoft]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-22 12:05:37
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Given an array of characters, compress it in-place.

The length after compression must always be smaller than or equal to the original array.

Every element of the array should be a character (not int) of length 1.

After you are done modifying the input array in-place, return the new length of the array.

 
Follow up:
Could you solve it using only O(1) extra space?

## Example
**Example 1:**
```
Input:
["a","a","b","b","c","c","c"]

Output:
Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]

Explanation:
"aa" is replaced by "a2". "bb" is replaced by "b2". "ccc" is replaced by "c3".
 
```
**Example 2:**
```
Input:
["a"]

Output:
Return 1, and the first 1 characters of the input array should be: ["a"]

Explanation:
Nothing is replaced.
```

**Example 3:**
```
Input:
["a","b","b","b","b","b","b","b","b","b","b","b","b"]

Output:
Return 4, and the first 4 characters of the input array should be: ["a","b","1","2"].

Explanation:
Since the character "a" does not repeat, it is not compressed. "bbbbbbbbbbbb" is replaced by "b12".
Notice each digit has it's own entry in the array.
```

**Note:**
1. All characters have an ASCII value in [35, 126].
2. 1 <= len(chars) <= 1000.

## Solution
```java
class Solution {
    public int compress(char[] chars) {
        int index = 0;
        int resIndex = 0;
        while(index < chars.length){
            char cur = chars[index];
            int count = 0;
            while(index < chars.length && cur == chars[index]){
                index++;
                count++;
            }
            chars[resIndex] = cur;
            resIndex++;
            if (count > 1){
                for (char ch: String.valueOf(count).toCharArray()){
                    chars[resIndex] = ch;
                    resIndex++;
                }
            }
        }
        return resIndex;
//         if (chars.length == 0) return 0;
//         char cur = chars[0];
//         int num = 1;
//         List<Character> res = new ArrayList<>();
//         for (int i = 1; i < chars.length; i++){
//             if (chars[i] == cur){
//                 num++;
//             }
//             else {
//                 res.add(cur);
//                 if (num > 1) {
//                     List<Character> tmp = new ArrayList<>();
//                     while(num > 0){
//                         char ch = (char)(num % 10 + 48);
//                         tmp.add(ch);
//                         num = num/10;
//                     }
//                     for (int j = tmp.size()-1; j>=0; j--) res.add(tmp.get(j));
//                 }
//                 cur = chars[i];
//                 num = 1;
//             }
//         }
//         res.add(cur);
//         if (num > 1){
//             List<Character> tmp = new ArrayList<>();
//             while(num > 0){
//                 char ch = (char)(num % 10 + 48);
//                 tmp.add(ch);
//                 num = num/10;    
//             }
//             for (int j = tmp.size() -1; j>=0; j--) res.add(tmp.get(j));
//         }
//         for (int i = 0; i < res.size(); i++) chars[i] = res.get(i);
        
//         return res.size();
    }
}
```

<hr />