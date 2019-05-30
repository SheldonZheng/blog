---
title: LeetCode 678 Valid Parenthesis String 有效的括号字符串 题解
date: 2019-05-15 17:20:24
tags:
---

题目地址

Description
Given a string containing only three types of characters: ‘(‘, ‘)’ and ‘*’, write a function to check whether this string is valid. We define the validity of a string by these rules:

Any left parenthesis '(' must have a corresponding right parenthesis ')'.
Any right parenthesis ')' must have a corresponding left parenthesis '('.
Left parenthesis '(' must go before the corresponding right parenthesis ')'.
'*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string.
An empty string is also valid.
Example 1:

Input: "()"
Output: True
Example 2:

Input: "(*)"
Output: True
Example 3:

Input: "(*))"
Output: True
Note:

The string size will be in the range [1, 100].
思路：
定义两个数，从0开始计数；

首先从左向右开始遍历，如果遇到*或者左括号，l 这个数+1，如果遇到右括号，-1；

循环每一次判断l是否小于0，如果有直接返回 false；

循环出来之后，如果l等于0 ，说明如果把所有的星号当做左括号，满足条件，返回true；

如果不等于0，继续判断，从右向左开始遍历，如果遇到*或者右括号，r+1，遇到左括号，r-1；

同样的，如果r小于0 ，直接返回false；

循环完之后，r不小于0就可以返回true；

对于r=0的情况，是把*都当做右括号，结果正好；

对于r>0的情况，把*都当做右括号，右括号会比左括号多；

但是如果把部分*当成空，右括号就不会多；

题解：
class Solution {
    public boolean checkValidString(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }
        int l = 0,r = 0;
        int n = s.length();
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) == '(' || s.charAt(i) == '*') {
                l++;
            } else {
                l--;
            }
            if (l < 0) {
                return false;
            }
        }

        if (l == 0) {
            return true;
        }

        for (int i = n - 1; i >= 0; i--) {
            if (s.charAt(i) == ')' || s.charAt(i) == '*') {
                r++;
            } else {
                r--;
            }
            if (r < 0) {
                return false;
            }
        }
        return true;
    }
}