---
title: Leetcode301-removeInvalidParentheses
categories: leetcode
tags: [DFS]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2020-03-16 22:42:50
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.

**Note**: The input string may contain letters other than the parentheses ( and ).

## Example
**Example 1:**
```
Input: "()())()"
Output: ["()()()", "(())()"]
```
**Example 2:**
```
Input: "(a)())()"
Output: ["(a)()()", "(a())()"]
```
**Example 3:**
```
Input: ")("
Output: [""]
```

## Solution

Solution 1

```java
class Solution {
// //     Basic method
    public List<String> removeInvalidParentheses(String s) {
        if (s == null || s.length() == 0) return Arrays.asList("");
        
//         preprocessor, count the number of alternative parentheses
        int numL = 0, numR = 0;
        for (char ch: s.toCharArray()){
            if (ch == '(')
                numL++;
            else if (ch == ')'){
                if (numL != 0)
                    numL --;
                else 
                    numR++;
            }
        }
        
        HashSet<String> set = new HashSet<>();
        helper(s, set, 0, "", numL, numR, 0);
        
        return new ArrayList<>(set);
    }
    private void helper(String s, HashSet<String> res, int idx, String cur, int numL, int numR, int open){
        if (numL < 0 || numR < 0 || open < 0)
            return;
        if (idx == s.length()){
            if (numL == 0 && numR == 0 && open == 0)
                res.add(new String(cur));
            return;
        }
        
        if (s.charAt(idx) == '('){
//             use '('
            helper(s, res, idx + 1, cur + "(", numL, numR, open + 1);
//             unuse '('
            helper(s, res, idx + 1, cur, numL - 1, numR, open);
        }
        else if (s.charAt(idx) == ')'){
//             use ')'
            helper(s, res, idx + 1, cur + ")", numL, numR, open - 1);
//             unuse ')'
            helper(s, res, idx + 1, cur, numL, numR - 1, open);
        }
        else helper(s, res, idx + 1, cur + s.charAt(idx), numL, numR, open);
    }
}
```

Solution 2

```java
class Solution {
// Generate unique answer once and only once, do not rely on Set.
// Do not need preprocess.
// Runtime 3 ms.
// Explanation:
// We all know how to check a string of parentheses is valid using a stack. Or even simpler use a counter.
// The counter will increase when it is ‘(‘ and decrease when it is ‘)’. Whenever the counter is negative, we have more ‘)’ than ‘(‘ in the prefix.

// To make the prefix valid, we need to remove a ‘)’. The problem is: which one? The answer is any one in the prefix. However, if we remove any one, we will generate duplicate results, for example: s = ()), we can remove s[1] or s[2] but the result is the same (). Thus, we restrict ourself to remove the first ) in a series of concecutive )s.

// After the removal, the prefix is then valid. We then call the function recursively to solve the rest of the string. However, we need to keep another information: the last removal position. If we do not have this position, we will generate duplicate by removing two ‘)’ in two steps only with a different order.
// For this, we keep tracking the last removal position and only remove ‘)’ after that.

// Now one may ask. What about ‘(‘? What if s = ‘(()(()’ in which we need remove ‘(‘?
// The answer is: do the same from right to left.
// However a cleverer idea is: reverse the string and reuse the code!
    public List<String> removeInvalidParentheses(String s) {
        List<String> ans = new ArrayList<>();
        remove(s, ans, 0, 0, new char[]{'(', ')'});
        return ans;
    }

    public void remove(String s, List<String> ans, int last_i, int last_j,  char[] par) {
        for (int stack = 0, i = last_i; i < s.length(); ++i) {
            if (s.charAt(i) == par[0]) stack++;
            if (s.charAt(i) == par[1]) stack--;
            if (stack >= 0) continue;
            for (int j = last_j; j <= i; ++j)
                if (s.charAt(j) == par[1] && (j == last_j || s.charAt(j - 1) != par[1]))
                    remove(s.substring(0, j) + s.substring(j + 1, s.length()), ans, i, j, par);
            return;
        }
        String reversed = new StringBuilder(s).reverse().toString();
        if (par[0] == '(') // finished left to right
            remove(reversed, ans, 0, 0, new char[]{')', '('});
        else // finished right to left
            ans.add(reversed);
}
}
```

<hr />