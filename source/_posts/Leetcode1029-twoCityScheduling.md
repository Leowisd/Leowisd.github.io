---
title: Leetcode1029-twoCityScheduling
categories: leetcode
tags: [Greedy, DP, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-01 23:28:54
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

There are 2N people a company is planning to interview. The cost of flying the i-th person to city A is costs[i][0], and the cost of flying the i-th person to city B is costs[i][1].

Return the minimum cost to fly every person to a city such that exactly N people arrive in each city.

## Example
```
Input: [[10,20],[30,200],[400,50],[30,20]]
Output: 110
Explanation: 
The first person goes to city A for a cost of 10.
The second person goes to city A for a cost of 30.
The third person goes to city B for a cost of 50.
The fourth person goes to city B for a cost of 20.

The total minimum cost is 10 + 30 + 50 + 20 = 110 to have half the people interviewing in each city.
```

**Note:**

* 1 <= costs.length <= 100
* It is guaranteed that costs.length is even.
* 1 <= costs[i][0], costs[i][1] <= 1000

## Solution

**Solution 1: DP**

$O(n^2)$, not the best

```java
class Solution {
    // dp[i][j] represents the cost when considering first (i + j) people in which i people assigned to city A and j people assigned to city B.
    public int twoCitySchedCost(int[][] costs) {
        int n = costs.length / 2;
        int[][] dp = new int[n + 1][n + 1];
        dp[0][0] = 0;
        for (int i = 1; i <= n; i++)
            dp[i][0] = dp[i - 1][0] + costs[i - 1][0];
        for (int j = 1; j <= n; j++)
            dp[0][j] = dp[0][j - 1] + costs[j - 1][1];
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
                dp[i][j] = Math.min(dp[i - 1][j] + costs[i + j - 1][0], dp[i][j - 1] + costs[i + j - 1][1]);
        return dp[n][n];
    }
}
```

**Solution 2: Greedy**

O(NlogN)

```java
class Solution {    
    // Greedy. If the dist to B is much longer than the dist to A, now the dif of dist to A and B could be very small and < 0. Therefore, we should assign these interviewees to A instead of B. So we sort the array by the difference of dist in ascending order and the first half are the interviewees assigned to A.
    public int twoCitySchedCost(int[][] costs) {
        Arrays.sort(costs, new Comparator<int[]>(){
            @Override
            public int compare(int[] a, int[] b){
                return (a[0] - a[1]) - (b[0] - b[1]);
            }
        });
        int res = 0;
        for (int i = 0; i < costs.length; i++){
            if (i < costs.length/2)
                res += costs[i][0];
            else res += costs[i][1];
        }
        return res;
    }
}
```

<hr />