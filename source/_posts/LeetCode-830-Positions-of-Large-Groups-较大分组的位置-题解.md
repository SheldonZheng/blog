---
title: LeetCode 830 Positions of Large Groups 较大分组的位置 题解
date: 2019-05-15 17:54:04
tags:
---

题目地址

830.Positions of Large Groups

Description
In a string S of lowercase letters, these letters form consecutive groups of the same character.

For example, a string like S = "abbxxxxzyy" has the groups "a", "bb", "xxxx", "z" and "yy".

Call a group large if it has 3 or more characters. We would like the starting and ending positions of every large group.

The final answer should be in lexicographic order.

Example 1:

Input: "abbxxxxzzy"
Output: [[3,6]]
Explanation: "xxxx" is the single large group with starting  3 and ending positions 6.
Example 2:

Input: "abc"
Output: []
Explanation: We have "a","b" and "c" but no large group.
Example 3:

Input: "abcdddeeeeaabbbcd"
Output: [[3,5],[6,9],[12,14]]
Note: 1 <= S.length <= 1000

题解
按顺序遍历一遍，找出大于三个的数就可以了。

class Solution {
    public List<List<Integer>> largeGroupPositions(String S) {
        List<List<Integer>> res = new ArrayList<>();
        if (S == null || S.length() == 0 || S.length() < 3) {
            return res;
        }
        char[] list = S.toCharArray();
        char p = list[0];
        int s = 0;
        int c = 0;
        for (int i = 0; i < list.length; i++) {
            if (p == list[i]) {
                c++;
            } else {
                p = list[i];
                if (c >= 3) {
                    List<Integer> temp = new ArrayList<>();
                    temp.add(s);
                    temp.add(i - 1);
                    res.add(temp);
                }
                c = 1;
                s = i;
            }
        }
        if (c >= 3) {
            List<Integer> temp = new ArrayList<>();
            temp.add(s);
            temp.add(list.length - 1);
            res.add(temp);
        }
        return res;
    }
}