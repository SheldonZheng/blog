---
title: LeetCode 816 Ambiguous Coordinates 模糊坐标 题解
date: 2019-05-15 17:19:23
tags:
---

题目地址

Description:
We had some 2-dimensional coordinates, like "(1, 3)" or "(2, 0.5)". Then, we removed all commas, decimal points, and spaces, and ended up with the string S. Return a list of strings representing all possibilities for what our original coordinates could have been.

Our original representation never had extraneous zeroes, so we never started with numbers like “00”, “0.0”, “0.00”, “1.0”, “001”, “00.01”, or any other number that can be represented with less digits. Also, a decimal point within a number never occurs without at least one digit occuring before it, so we never started with numbers like “.1”.

The final answer list can be returned in any order. Also note that all coordinates in the final answer have exactly one space between them (occurring after the comma.)

Example 1:
Input: "(123)"
Output: ["(1, 23)", "(12, 3)", "(1.2, 3)", "(1, 2.3)"]
Example 2:
Input: "(00011)"
Output:  ["(0.001, 1)", "(0, 0.011)"]
Explanation: 
0.0, 00, 0001 or 00.01 are not allowed.
Example 3:
Input: "(0123)"
Output: ["(0, 123)", "(0, 12.3)", "(0, 1.23)", "(0.1, 23)", "(0.1, 2.3)", "(0.12, 3)"]
Example 4:
Input: "(100)"
Output: [(10, 0)]
Explanation: 
1.0 is not allowed.
Note:

4 <= S.length <= 12.
S[0] = “(“, S[S.length - 1] = “)”, and the other elements in S are digits.
题解:
首先要明确对于一个字符串，有几种不允许出现的情况，实现一个函数，依次判断这些特殊情况，之后剩下的就是将小数点从前往后依次挪，将每一种可能性合并在一起；

将给的字符串分成两部分，从循环求解所有的可能性；

class Solution {
     public List<String> ambiguousCoordinates(String S) {
        int l = S.length();
        List<String> res = new ArrayList<>();
        for (int i = 1; i < l - 2; i++) {
            List<String> tempA = find(S.substring(1, i + 1));
            List<String> tempB = find(S.substring(i + 1,l - 1));

            //merge
            tempA.forEach((a) -> {
                tempB.forEach((b) -> {
                    res.add("(".concat(a).concat(", ").concat(b).concat(")"));
                });
            });
        }
        return res;
    }

    public List<String> find(String s) {
        int l = s.length();
        List<String> res = new ArrayList<>();
        //0XXX0
        if (l == 0 || (l > 1 && s.charAt(0) == '0' && s.charAt(l - 1) == '0')) {
            return res;
        }

        //0XXX
        if (l > 1 && s.charAt(0) == '0') {
            res.add("0.".concat(s.substring(1,l)));
            return res;
        }
        res.add(s);
        //X
        if (l == 1) {
            return res;
        }
        //XXX0
        if (s.charAt(l - 1) == '0') {
            return res;
        }

        for (int i = 1; i < l; i++) {
            res.add(s.substring(0,i).concat(".").concat(s.substring(i,l)));
        }
        return res;

    }
}