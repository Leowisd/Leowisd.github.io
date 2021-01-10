---
title: Leetcode068-Text Justification
categories: leetcode
tags: [String, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-10 02:52:49
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
Given an array of words and a width maxWidth, format the text such that each line has exactly maxWidth characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly maxWidth characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no extra space is inserted between words.

**Note:**

* A word is defined as a character sequence consisting of non-space characters only.
* Each word's length is guaranteed to be greater than 0 and not exceed maxWidth.
* The input array words contains at least one word.

## Example

**Example 1:**
```
Input: words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16
Output:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```
**Example 2:**
```
Input: words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16
Output:
[
  "What   must   be",
  "acknowledgment  ",
  "shall be        "
]
Explanation: Note that the last line is "shall be    " instead of "shall     be", because the last line must be left-justified instead of fully-justified.
Note that the second line is also left-justified becase it contains only one word.
```
**Example 3:**
```
Input: words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20
Output:
[
  "Science  is  what we",
  "understand      well",
  "enough to explain to",
  "a  computer.  Art is",
  "everything  else  we",
  "do                  "
]
``` 

**Constraints:**

* 1 <= words.length <= 300
* 1 <= words[i].length <= 20
* words[i] consists of only English letters and symbols.
* 1 <= maxWidth <= 100
* words[i].length <= maxWidth

## Solution

* Time Complexity: $$O(N)$$
* Space Complexity: $$O(len(res))$$
```
We start with left being the first word.

findRight: Then we greedily try to go as far right as possible until we fill our current line.

Then we justify one line at a time.

justify: In all cases we pad the right side with spaces until we reach max width for the line;

If it's one word then it is easy, the result is just that word.
If it's the last line then the result is all words separated by a single space.
Otherwise we calculate the size of each space evenly and if there is a remainder we distribute an extra space until it is gone.
```

```java
class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        int cur = 0; 
        List<String> res = new ArrayList<>();
        
        while (cur < words.length) {
            int curEnd = find(cur, words, maxWidth);
            res.add(justify(cur, curEnd, words, maxWidth));
            cur = curEnd + 1;
        }
        
        return res;
    }
    
    private int find(int cur, String[] words, int maxWidth) {
        int curEnd = cur;
        int sum = words[curEnd++].length();
        
        while (curEnd < words.length && (sum + 1 + words[curEnd].length()) <= maxWidth)
            sum += 1 + words[curEnd++].length();
            
        return curEnd - 1;
    }
    
    private String justify(int cur, int curEnd, String[] words, int maxWidth) {
        if (curEnd == cur) return pad(words[cur], maxWidth);
        
        boolean isLastLine = curEnd == words.length - 1;
        int numWords = curEnd - cur;
        int totalSpace = maxWidth - wordsLength(cur, curEnd, words);       
        int numSpaces = isLastLine ? 1 : totalSpace / numWords;
        int remainder = isLastLine ? 0 : totalSpace % numWords;
        
        StringBuilder res = new StringBuilder();
        for (int i = cur; i < curEnd; i++){
            res.append(words[i]);
            res.append(whitespace(numSpaces));
            res.append(remainder-- > 0 ? " " : "");
        }
        res.append(words[curEnd]);
        
        return isLastLine ? pad(res.toString(), maxWidth) : res.toString();
    }
    
        private String pad(String s, int maxWidth) {
        StringBuilder sb = new StringBuilder(s);
        sb.append(whitespace(maxWidth - s.length()));
        return sb.toString();
    }
    
    private String whitespace(int length) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < length; i++) {
            sb.append(" ");
        }
        return sb.toString();
    }
    
    private int wordsLength(int cur, int curEnd, String[] words) {
        int wordsLength = 0;
        for (int i = cur; i <= curEnd; i++) {
            wordsLength += words[i].length();
        }
        return wordsLength;
    }
}
```

<hr />