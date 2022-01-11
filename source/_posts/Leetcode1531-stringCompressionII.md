---
title: Leetcode1531-String Compression II
categories: leetcode
tags: [DP, Google]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2022-01-10 23:05:20
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Run-length encoding is a string compression method that works by replacing consecutive identical characters (repeated 2 or more times) with the concatenation of the character and the number marking the count of the characters (length of the run). For example, to compress the string "aabccc" we replace "aa" by "a2" and replace "ccc" by "c3". Thus the compressed string becomes "a2bc3".

Notice that in this problem, we are not adding '1' after single characters.

Given a string s and an integer k. You need to delete at most k characters from s such that the run-length encoded version of s has minimum length.

Find the minimum length of the run-length encoded version of s after deleting at most k characters.

## Example

**Example 1:**
```
Input: s = "aaabcccd", k = 2
Output: 4
Explanation: Compressing s without deleting anything will give us "a3bc3d" of length 6. Deleting any of the characters 'a' or 'c' would at most decrease the length of the compressed string to 5, for instance delete 2 'a' then we will have s = "abcccd" which compressed is abc3d. Therefore, the optimal way is to delete 'b' and 'd', then the compressed version of s will be "a3c3" of length 4.
```

**Example 2:**
```
Input: s = "aabbaa", k = 2
Output: 2
Explanation: If we delete both 'b' characters, the resulting compressed string would be "a4" of length 2.
```
**Example 3:**
```
Input: s = "aaaaaaaaaaa", k = 0
Output: 3
Explanation: Since k is zero, we cannot delete anything. The compressed string is "a11" of length 3.
```

**Constraints:**

* 1 <= s.length <= 100
* 0 <= k <= s.length
* s contains only lowercase English letters.

## Solution

* Time Complexity: $$O(n^2k)$$
* Space Complexity: $$O(nk)$$

```java
// We define the state dp[i][k]: the minimum length for s.substring(0, i+1) with at most k deletion.
// For each char s[i], we can either keep it or delete it.
// If delete, dp[i][j]=dp[i-1][j-1].
// If keep, we delete at most j chars in s.substring(0, i+1) that are different from s[i].
// O(kn^2)
// 状态定义：T(i, k) 表示 [i, n) 范围内、最多可删除 k 个字符的最优解

// 状态转移：

// 删除字符。T(i+1, k-1)，if k > 0
// 保留字符。枚举以 s[i] 为首的字符组的所有可能结束位置 j，encodeOne(sameCount([i, j+1))) + T(j+1, k - diffCount([i, j+1))，if k - diffCount([i, j+1) >= 0
// 其中，sameCount([i, j+1)) 表示 [i, j+1) 范围内与 s[i] 相同的字符个数，则 diffCount([i, j+1)) = (j+1-i) - sameCount([i, j+1)) 为 [i, j+1) 内与 s[i] 不同的字符个数，即 [i, j+1) 内被删除的字符个数
class Solution {
    public int getLengthOfOptimalCompression(String s, int k) {
        int n = s.length();
        int[][] dp = new int[n + 1][k + 1];
        
        for (int i = 0; i <= n; i++){
            for (int j = 0; j <= k; j++){
                dp[i][j] = 10000;
            }
        }
        
        
        dp[0][0] = 0;
        for (int i = 1; i <= n; i++){
            for (int j = 0; j <= k; j++){
                int count = 0;
                int delete = 0;
                for (int m = i; m >= 1; m--){
                    if (s.charAt(m - 1) == s.charAt(i - 1)){
                        count++;
                    }
                    else{
                        delete++;
                    }
                    if (j - delete >= 0){
                        dp[i][j] = Math.min(dp[i][j], dp[m - 1][j - delete] + 1 + (count >= 100 ? 3 : count >= 10 ? 2 : count >= 2 ? 1 : 0));
                    }
                }
                if (j > 0){
                    dp[i][j] = Math.min(dp[i][j], dp[i - 1][j - 1]);
                }
            }
        }

        return dp[n][k];
    }
}
```

<hr />