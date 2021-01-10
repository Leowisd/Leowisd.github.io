---
title: Leetcode1155-Number of Dice Rolls With Target Sum
categories: leetcode
tags: [DP, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2021-01-10 00:31:06
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

You have d dice, and each die has f faces numbered 1, 2, ..., f.

Return the number of possible ways (out of fd total ways) modulo **10^9 + 7** to roll the dice so the sum of the face up numbers equals target.

## Example

**Example 1:**
```
Input: d = 1, f = 6, target = 3
Output: 1
Explanation: 
You throw one die with 6 faces.  There is only one way to get a sum of 3.
```
**Example 2:**
```
Input: d = 2, f = 6, target = 7
Output: 6
Explanation: 
You throw two dice, each with 6 faces.  There are 6 ways to get a sum of 7:
1+6, 2+5, 3+4, 4+3, 5+2, 6+1.
```
**Example 3:**
```
Input: d = 2, f = 5, target = 10
Output: 1
Explanation: 
You throw two dice, each with 5 faces.  There is only one way to get a sum of 10: 5+5.
```
**Example 4:**
```
Input: d = 1, f = 2, target = 3
Output: 0
Explanation: 
You throw one die with 2 faces.  There is no way to get a sum of 3.
```
**Example 5:**
```
Input: d = 30, f = 30, target = 500
Output: 222616187
Explanation: 
The answer must be returned modulo 10^9 + 7.
```

**Constraints:**
```
1 <= d, f <= 30
1 <= target <= 1000
```
## Solution

### Solution 1: 2-D DP

* Time Complexity: $$O(d * f * target)$$
* Space Complexity: $$O(d * target)$$

```java
class Solution {
    public int numRollsToTarget(int d, int f, int target) {
        int MOD = (int)Math.pow(10, 9) + 7;
        //how many possibility can i dices sum up to j;
        int[][] dp = new int[d + 1][target + 1];
        dp[0][0] = 1;
        for (int i = 1; i <= d; i++){
            for (int j = 1; j <= target; j++){
                if (j > i * target){
                    break;
                }
                for (int k = 1; k <= f && k <= j; k++){
                    dp[i][j] = (dp[i][j] + dp[i - 1][j - k]) % MOD;
                }
            }
        }
        return dp[d][target];
    }
}
```
### Solution 2: 1-D DP

* Time Complexity: $$O(d * f * target)$$
* Space Complexity: $$O(target)$$
  
```java
class Solution {
    public int numRollsToTarget(int d, int f, int target) {
        int MOD = (int)Math.pow(10, 9) + 7;
    	int[] dp = new int[target+1];
    	dp[0] = 1;
    	for(int i = 1;i <= d;i++) {
    		int []temp = new int[target+1];
    		for(int j = 1;j <= target;j++) {
    			if(j > i * f)
    				break;
				for(int k = 1;k <= f && k <= j;k++)
					temp[j] = (temp[j] + dp[j - k]) % MOD;
    		}
    		dp = temp;
    	}
    	return dp[target];
    }
}
```

### Solution 3: DFS with memoery
```java
class Solution {
    int MOD = (int)Math.pow(10, 9) + 7;
    Map<String, Integer> memo = new HashMap<>();
    public int numRollsToTarget(int d, int f, int target) {
        if (d == 0 && target == 0){
            return 1;
        }
        if (d == 0 || target == 0){
            return 0;
        }
        String key = d + " " + target;
        if (memo.containsKey(key)) return memo.get(key);
        int res = 0;
        for (int i = 1; i <= f; i++){
            if (i > target){
                break;
            }
            res = (res + numRollsToTarget(d - 1, f, target - i)) % MOD;
        }
        memo.put(key, res);
        return res;
    }
}
```

<hr />