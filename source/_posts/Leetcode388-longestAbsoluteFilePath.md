---
title: Leetcode388-longestAbsoluteFilePath
categories: leetcode
tags: [Stack, Amazon]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-14 10:22:00
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Suppose we abstract our file system by a string in the following manner:

The string "dir\n\tsubdir1\n\tsubdir2\n\t\tfile.ext" represents:
```
dir
    subdir1
    subdir2
        file.ext
```

The directory dir contains an empty sub-directory subdir1 and a sub-directory subdir2 containing a file file.ext.

The string "dir\n\tsubdir1\n\t\tfile1.ext\n\t\tsubsubdir1\n\tsubdir2\n\t\tsubsubdir2\n\t\t\tfile2.ext" represents:
```
dir
    subdir1
        file1.ext
        subsubdir1
    subdir2
        subsubdir2
            file2.ext
```
The directory dir contains two sub-directories subdir1 and subdir2. subdir1 contains a file file1.ext and an empty second-level sub-directory subsubdir1. subdir2 contains a second-level sub-directory subsubdir2 containing a file file2.ext.

We are interested in finding the longest (number of characters) absolute path to a file within our file system. For example, in the second example above, the longest absolute path is "dir/subdir2/subsubdir2/file2.ext", and its length is 32 (not including the double quotes).

Given a string representing the file system in the above format, return the length of the longest absolute path to file in the abstracted file system. If there is no file in the system, return 0.

**Note:**
* The name of a file contains at least a . and an extension.
* The name of a directory or sub-directory will not contain a ..
* Time complexity required: O(n) where n is the size of the input string.

Notice that a/aa/aaa/file1.txt is not the longest file path, if there is another path aaaaaaaaaaaaaaaaaaaaa/sth.png.

## Solution
```java
class Solution {
    public int lengthLongestPath(String input) {
        int res = 0;
        if (input == null || input.length() == 0) return res;
        
        Stack<Integer> st = new Stack<>();
        st.push(0);
        
        for (String cur: input.split("\n")){
            int level = cur.lastIndexOf("\t") + 1; // number of "\t"
            while(level + 1 < st.size()) st.pop(); // find parent
            int len = st.peek() + cur.length() - level + 1; // remove "/t", add"/"
            st.push(len);
            if (cur.contains(".")) res = Math.max(res, len - 1);
        }         
        
        return res;
    }
}
```

<hr />