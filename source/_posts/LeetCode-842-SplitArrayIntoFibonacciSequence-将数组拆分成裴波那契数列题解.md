---
title: LeetCode.842.SplitArrayIntoFibonacciSequence.将数组拆分成裴波那契数列题解
date: 2019-05-15 17:54:53
tags:
---

题目地址

842.Split Array into Fibonacci Sequence

Given a string S of digits, such as S = "123456579", we can split it into a Fibonacci-like sequence [123, 456, 579].

Formally, a Fibonacci-like sequence is a list F of non-negative integers such that:

0 <= F[i] <= 2^31 - 1, (that is, each integer fits a 32-bit signed integer type);
F.length >= 3;
andF[i] + F[i+1] = F[i+2]for all 0 <= i < F.length - 2.
Also, note that when splitting the string into pieces, each piece must not have extra leading zeroes, except if the piece is the number 0 itself.

Return any Fibonacci-like sequence split from S, or return [] if it cannot be done.

Example 1:

Input: "123456579"
Output: [123,456,579]
Example 2:

Input: "11235813"
Output: [1,1,2,3,5,8,13]
Example 3:

Input: "112358130"
Output: []
Explanation: The task is impossible.
Example 4:

Input: "0123"
Output: []
Explanation: Leading zeroes are not allowed, so "01", "2", "3" is not valid.
Example 5:

Input: "1101111"
Output: [110, 1, 111]
Explanation: The output [11, 0, 11, 11] would also be accepted.
Note:

1 <= S.length <= 200
S contains only digits.
解题思路
看到题目的第一反应是在一个无序数组里找数来拼成裴波那契数列，那这个有点难，没想到什么办法；

然后看了几个例子，发现是在有序数组里寻找，一下子简单很多；

用回溯法；

回溯法的详细解释，请点击上面的链接；

简单来说，就是一步一步地尝试解，如果不行，就回退；

​ 举个例子，我们首先把数组的第一位添加到结果集里，然后把第二位也添加到结果集里，发现第三位不等于前两位之和，这时候就得回退，不能用第一位和第二位啦，删除结果集里已有的这两个数，尝试把第一位和第二位作为一个数放到结果集里，然后把第三位也放进去，判断第四位是否等于前两个数的和……

代码:

class Solution {
    public List<Integer> splitIntoFibonacci(String S) {
        List<Integer> res = new ArrayList<>();
        if (S == null || S.length() == 0) {
            return res;
        }
        dfs(S,res,0);
        return res;

    }

    private boolean dfs(String S,List<Integer> res,int index) {
        //已有解，可以返回了
        if (S.length() == index && res.size() >= 3) {
            return true;
        }
        for (int i = index; i < S.length(); i++) {
            if (S.charAt(index) == '0' && i > index) {
                return false;
            }
            Long num = Long.parseLong(S.substring(index,i + 1));
            //超出范围了
            if (num > Integer.MAX_VALUE) {
                return false;
            }

            //数组里有两个以上的数，判断这个数能不能符合要求
            if (res.size() >= 2 && (num > res.get(res.size() - 1) + res.get(res.size() - 2))) {
                return false;
            }

            //还不到两个数，或者符合要求，添加进去，继续往前走
            if (res.size() < 2 || (num == res.get(res.size() - 1) + res.get(res.size() - 2))) {
                res.add(num.intValue());
                if (dfs(S,res,i + 1)) {
                    return true;
                }
                //删除刚加进去的，回头
                res.remove(res.size() - 1);
            }
        }
        return false;
    }
}