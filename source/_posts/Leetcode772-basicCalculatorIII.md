---
title: Leetcode772-basicCalculatorIII
categories: leetcode
tags: [Stack, String, Amazon, TikTok]
description: Solution Report of LeetCode Acceptted
mathjax: true
date: 2019-10-04 18:12:50
permalink:
image:
---
<p class="description"></p>

<img src="/images/LeetCode.jpg" alt="" style="width:100%" /> <!-- 首页和文章内都会显示 -->

<!-- more -->

## Description

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open ( and closing parentheses ), the plus + or minus sign -, non-negative integers and empty spaces .

The expression string contains only non-negative integers, +, -, *, / operators , open ( and closing parentheses ) and empty spaces . The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of [-2147483648, 2147483647].

## Example
```
"1 + 1" = 2
" 6-4 / 2 " = 4
"2*(5+5*2)/3+(6/2+8)" = 21
"(2+6* 3+5- (3*14/7+2)*5)+3"=-12
```

## Solution
```java
class Solution {
//  More easy to understand
    public int calculate(String s) {
        if (s == null) {
            return 0;
        }    
        Queue<Character> q = new LinkedList<>();
        for (char c : s.toCharArray()) {
            q.offer(c);
        }
        q.offer('+');
        return cal(q);
    }
    
    private int cal(Queue<Character> q) {
        char sign = '+';
        int num = 0;
        Stack<Integer> stack = new Stack<>();
        while (!q.isEmpty()) {
            char c = q.poll();
            if (c == ' ') {
                continue;
            }
            if (Character.isDigit(c)) {
                num = 10 * num + c - '0';
            } else if (c == '(') {
                num = cal(q);
            } else {
                if (sign == '+') {
                    stack.push(num);
                } else if (sign == '-') {
                    stack.push(-num);
                } else if (sign == '*') {
                    stack.push(stack.pop() * num);
                } else if (sign == '/') {
                    stack.push(stack.pop() / num);
                }
                num = 0;
                sign = c;
                if (c == ')') {
                    break;
                }
            }
        }
        int sum = 0;
        while (!stack.isEmpty()) {
            sum += stack.pop();
        }
        return sum;
    }
//     public int calculate(String s) {
//         int l1 = 0, o1 = 1;
//         int l2 = 1, o2 = 1;
//         Stack<Integer> st = new Stack<>();
//         int i = 0;
//         while (i < s.length()){
//             char c = s.charAt(i);
//             if (Character.isDigit(c)){
//                 int num = c - '0';
//                 while(i+1<s.length() && Character.isDigit(s.charAt(i+1))){
//                     num = num * 10 + (s.charAt(++i) - '0');
//                 }
//                 l2 = (o2 == 1 ? l2 * num : l2 / num);
//             }
//             else if (c == '('){
//                 st.push(l1);
//                 st.push(o1);
//                 st.push(l2);
//                 st.push(o2);
//                 l1 = 0; o1 = 1;
//                 l2 = 1; o2 = 1;
//             }
//             else if (c == ')'){
//                 int num = l1 + o1 * l2;
//                 o2 = st.pop(); l2 = st.pop();
//                 o1 = st.pop(); l1 = st.pop();
//                 l2 = (o2 == 1 ? l2 * num : l2 / num);
//             }
//             else if (c == '*' || c == '/'){
//                o2 = (c == '*' ? 1 : -1); 
//             }
//             else if (c == '+' || c == '-'){
//                 if (c == '-' && (i == 0 || s.charAt(i - 1) == '(')) {
//                     o1 = -1;
//                 }
//                 else{
//                     l1 = l1 + o1 * l2;
//                     o1 = (c == '+' ? 1 : -1);
                
//                     l2 = 1;
//                     o2 = 1;   
//                 }
//             }
//             i++;
//         }
//         return l1+o1*l2;
//     }
}
```
Time Complex: $O(N)$ for both above

<hr />