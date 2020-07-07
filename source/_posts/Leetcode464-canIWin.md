---
title: Leetcode464-canIWin
categories: leetcode
tags: [DP]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-02-22 21:05:13
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

In the "100 game," two players take turns adding, to a running total, any integer from 1..10. The player who first causes the running total to reach or exceed 100 wins.

What if we change the game so that players cannot re-use integers?

For example, two players might take turns drawing from a common pool of numbers of 1..15 without replacement until they reach a total >= 100.

Given an integer maxChoosableInteger and another integer desiredTotal, determine if the first player to move can force a win, assuming both players play optimally.

You can always assume that maxChoosableInteger will not be larger than 20 and desiredTotal will not be larger than 300.

## Example
```
Input:
maxChoosableInteger = 10
desiredTotal = 11

Output:
false

Explanation:
No matter which integer the first player choose, the first player will lose.
The first player can choose an integer from 1 up to 10.
If the first player choose 1, the second player can only choose integers from 2 up to 10.
The second player will win by choosing 10 and get a total = 11, which is >= desiredTotal.
Same with other integers chosen by the first player, the second player will always win.
```

## Solution
```java
class Solution {
    public boolean canIWin(int maxChoosableInteger, int desiredTotal) {
        if (desiredTotal <= 0) return true;
        // 1 + 2 + ... + maxChoosableInteger < desiredTotal means can't reach to desiredTotal
        if (maxChoosableInteger * (maxChoosableInteger + 1) / 2 < desiredTotal) return false;
        int[] dp = new int[1 << maxChoosableInteger];
        return dfs(dp, 0, maxChoosableInteger, desiredTotal);
    }
    
    public boolean dfs(int[] dp, int chs, int max, int target) {
        // targer <= 0 means the prior one wins
        if (target <= 0) return false;
        if (dp[chs] != 0) return dp[chs] == 1;
        boolean win = false;
        for (int i = 0; i < max; i++) {
            // i + 1 not use
            if ((chs & (1 << i)) == 0) {
                // thers is a trick: short circuit, when win is true, the next dfs won't be invoke
                win = win || !dfs(dp, chs ^ (1 << i), max, target - i - 1);
            }
        }
        dp[chs] = win ? 1 : -1;
        return win;
    }
}
```

<hr />