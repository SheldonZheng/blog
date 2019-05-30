---
title: LeetCode 795 Number of Subarrays with BoundedMaximum 区间子数组个数 题解
date: 2019-05-15 17:18:58
tags:
---

题目地址

Description:
We are given an array A of positive integers, and two positive integers L and R (L <= R).

Return the number of (contiguous, non-empty) subarrays such that the value of the maximum array element in that subarray is at least Land at most R.

Example :
Input: 
A = [2, 1, 4, 3]
L = 2
R = 3
Output: 3
Explanation: There are three subarrays that meet the requirements: [2], [2, 1], [3].
Note:

L, R and A[i] will be an integer in the range [0, 10^9].
The length of A will be in the range of [1, 50000].
题解：
注意审题，题目中说，连续、非空、且 “最大元素”满足 >= L <=R，只要最大元素满足就可以了；

定义一个maxL，最大长度，即包含一个最大元素 满足要求的 子数组的 最大长度

定义一个lp ，left point 左指针

右指针先往前挪，如果数满足条件，更新结果集和maxL的值

如果数小于L，那么更新结果集，加上maxL的数

如果是别的情况，重置maxL，将左指针挪到跟右指针相同的位置

class Solution {
    public int numSubarrayBoundedMax(int[] A, int L, int R) {
        if (A == null || A.length == 0) {
            return 0;
        }
        //left point
        int lp = 0;
        int res = 0;

        int maxL = 0;
        //right point
        for (int rp = 0; rp < A.length; rp++) {
            if (A[rp] >= L && A[rp] <= R) {
                res += (rp - lp + 1);
                maxL = (rp - lp + 1);
            } else if (A[rp] < L) {
                res += maxL;
            } else {
                //reset maxL
                maxL = 0;
                //move left point
                lp = rp + 1;
            }
        }
        return res;
    }
}
