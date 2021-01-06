---
title: Leetcode465-optimalAccountBalancing
categories: leetcode
tags: [DFS, Google, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-04-07 17:42:25
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description
A group of friends went on holiday and sometimes lent each other money. For example, Alice paid for Bill's lunch for $10. Then later Chris gave Alice $5 for a taxi ride. We can model each transaction as a tuple (x, y, z) which means person x gave person y $z. Assuming Alice, Bill, and Chris are person 0, 1, and 2 respectively (0, 1, 2 are the person's ID), the transactions can be represented as [[0, 1, 10], [2, 0, 5]].

Given a list of transactions between a group of people, return the minimum number of transactions required to settle the debt.

**Note:**

1. A transaction will be given as a tuple (x, y, z). Note that x ≠ y and z > 0.
2. Person's IDs may not be linear, e.g. we could have the persons 0, 1, 2 or we could also have the persons 0, 2, 6.

## Example
**Example 1:**
```
Input:
[[0,1,10], [2,0,5]]

Output:
2

Explanation:
Person #0 gave person #1 $10.
Person #2 gave person #0 $5.

Two transactions are needed. One way to settle the debt is person #1 pays person #0 and #2 $5 each.
```
**Example 2:**
```
Input:
[[0,1,10], [1,0,1], [1,2,5], [2,0,5]]

Output:
1

Explanation:
Person #0 gave person #1 $10.
Person #1 gave person #0 $1.
Person #1 gave person #2 $5.
Person #2 gave person #0 $5.

Therefore, person #1 only need to give person #0 $4, and all debt is settled.
```

## Solution
With all the given transactions, in the end, each person with ID = id will have an overall balance bal[id]. Note that the id value or any person coincidentally with 0 balance is irrelevant to debt settling count, so we can simply use an array debt[] to store all non-zero balances, where
* debt[i] > 0 means a person needs to pay $ debt[i] to other person(s);
* debt[i] < 0 means a person needs to collect $ debt[i] back from other person(s).

Starting from first debt debt[0], we look for all other debts debt[i] (i>0) which have opposite sign to debt[0]. Then each such debt[i] can make one transaction debt[i] += debt[0] to clear the person with debt debt[0]. From now on, the person with debt debt[0] is dropped out of the problem and we recursively drop persons one by one until everyone's debt is cleared meanwhile updating the minimum number of transactions during DFS.

Worest Time: O(n!), factorial of n
```java
class Solution {
    public int minTransfers(int[][] transactions) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int[] trans: transactions){
            map.put(trans[0], map.getOrDefault(trans[0], 0) - trans[2]);
            map.put(trans[1], map.getOrDefault(trans[1], 0) + trans[2]);
        }
//      sort can improve speed
        List<Integer> debt = new ArrayList<>(map.values());
        Collections.sort(debt);
//      -----------------------
        return helper(0, debt);
    }
    private int helper(int cur, List<Integer> debt){
        while(cur < debt.size() && debt.get(cur) == 0)
            cur++;
        if (cur == debt.size())
            return 0;
        int res = Integer.MAX_VALUE;
        for (int i = cur + 1; i < debt.size(); i++){
            if (debt.get(cur) * debt.get(i) < 0){
                debt.set(i, debt.get(i) + debt.get(cur));
                res = Math.min(res, 1 + helper(cur + 1, debt));
                debt.set(i, debt.get(i) - debt.get(cur));
            }
        }
        return res;
    }
}
```

<hr />