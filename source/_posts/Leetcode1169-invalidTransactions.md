---
title: Leetcode1169-invalidTransactions
categories: leetcode
tags: [String, Array, Hash Table, Bloomberg]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-01 23:24:46
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

A transaction is possibly invalid if:

the amount exceeds $1000, or;
if it occurs within (and including) 60 minutes of another transaction with the same name in a different city.
Each transaction string transactions[i] consists of comma separated values representing the name, time (in minutes), amount, and city of the transaction.

Given a list of transactions, return a list of transactions that are possibly invalid.  You may return the answer in any order.

## Example
**Example 1:**
```
Input: transactions = ["alice,20,800,mtv","alice,50,100,beijing"]
Output: ["alice,20,800,mtv","alice,50,100,beijing"]
Explanation: The first transaction is invalid because the second transaction occurs within a difference of 60 minutes, have the same name and is in a different city. Similarly the second one is invalid too.
```
**Example 2:**
```
Input: transactions = ["alice,20,800,mtv","alice,50,1200,mtv"]
Output: ["alice,50,1200,mtv"]
```
**Example 3:**
```
Input: transactions = ["alice,20,800,mtv","bob,50,1200,mtv"]
Output: ["bob,50,1200,mtv"]
```

**Constraints:**

* transactions.length <= 1000
* Each transactions[i] takes the form "{name},{time},{amount},{city}"
* Each {name} and {city} consist of lowercase English letters, and have lengths between 1 and 10.
* Each {time} consist of digits, and represent an integer between 0 and 1000.
* Each {amount} consist of digits, and represent an integer between 0 and 2000.

## Solution
```java
// Map
// Key: Name
// Value: List of {time, amount, city}
// 
// once new transaction come under one name
// check amount first, 
// then if in differnt cities, check if time invalid 

// Define a custmized class to store history imfomation, it can save time of spliting each time

class Solution {
    class Transaction{
        String name;
        int time;
        String city;
        String trans;
        public Transaction(String name, int time, String city, String trans){
            this.name = name;
            this.time = time;
            this.city = city;
            this.trans = trans;
        }
    }
    public List<String> invalidTransactions(String[] transactions) {
        HashMap<String, List<Transaction>> map = new HashMap<>();
        if (transactions == null || transactions.length == 0) return new ArrayList<>();
        
        HashSet<String> invalid = new HashSet<>();
        for (String transaction: transactions){
            String[] cur = transaction.split(",");
            String name = cur[0];
            int time = Integer.valueOf(cur[1]);
            int amount = Integer.valueOf(cur[2]);
            String city = cur[3];
//             Check if amount invalid
            if (amount > 1000)
                invalid.add(transaction);
            
            if (!map.containsKey(name))
                map.put(name, new ArrayList<Transaction>());
            
            for (Transaction history: map.get(name)){
//                 Check if in different cities
                if (!history.city.equals(cur[3])){
//                     Check if time invalid
                    if (Math.abs(time - history.time) <= 60){
                        invalid.add(transaction);
                        invalid.add(history.trans);
                    }
                }
            }
            map.get(name).add(new Transaction(name, time, city, transaction));
        }
        
        return new ArrayList<String>(invalid);
    }
}
```

<hr />