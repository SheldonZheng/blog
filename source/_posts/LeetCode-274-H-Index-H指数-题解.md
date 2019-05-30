---
title: LeetCode.274.H-Index.H指数.题解
date: 2019-05-15 17:19:47
tags:
---

题目地址

Description:
Given an array of citations (each citation is a non-negative integer) of a researcher, write a function to compute the researcher’s h-index.

According to the definition of h-index on Wikipedia: “A scientist has index h if h of his/her N papers have at least h citations each, and the other N − h papers have no more than h citations each.”

Example:

Input: citations = [3,0,6,1,5]
Output: 3 
Explanation: [3,0,6,1,5] means the researcher has 5 papers in total and each of them had 
             received 3, 0, 6, 1, 5 citations respectively. 
             Since the researcher has 3 papers with at least 3 citations each and the remaining 
             two with no more than 3 citations each, her h-index is 3.
Note: If there are several possible values for h, the maximum one is taken as the h-index.

题解：
定义一个新的数组，用来存储 引用次数出现的次数；

设新数组为hash，hash[i] 就是 i 出现的次数

比如输入 citations = [3,0,3,0,2,0,3] ， hash[3] 的值就会是3，出现了三次；

如果记录出现次数的时候，出现了引用次数比所有文章的数量多的数，比如一共发表5篇文章，有一篇文章引用数量是6次，那应该把这个六次记到hash[5]的地方，假设他引用了5次来处理；因为h指数不能大于文章数量；

然后从数组的后面向前扫描，前一个数的引用次数是后面所有的数加起来的值；判断如果有引用次数大于等于当前数的，那这个数就是h指数了。

class Solution {
    public int hIndex(int[] citations) {
        if (citations == null || citations.length == 0) {
            return 0;
        }

        int[] hash = new int[citations.length + 1];
        for (int i : citations) {
            if (i >= citations.length) {
                hash[citations.length]++;
            } else {
                hash[i]++;
            }
        }

        for (int i = hash.length - 1; i > 0; i--) {
            if (hash[i] >= i) {
                return i;
            }
            hash[i - 1] += hash[i];
        }
        return 0;
    }
}