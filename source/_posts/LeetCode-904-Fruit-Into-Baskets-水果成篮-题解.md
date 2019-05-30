---
title: LeetCode 904 Fruit Into Baskets 水果成篮 题解
date: 2019-05-15 17:54:25
tags:
---

题目地址

904.Fruit Into Baskets

Description
In a row of trees, the i-th tree produces fruit with type tree[i].

You start at any tree of your choice, then repeatedly perform the following steps:

Add one piece of fruit from this tree to your baskets. If you cannot, stop.
Move to the next tree to the right of the current tree. If there is no tree to the right, stop.
Note that you do not have any choice after the initial choice of starting tree: you must perform step 1, then step 2, then back to step 1, then step 2, and so on until you stop.

You have two baskets, and each basket can carry any quantity of fruit, but you want each basket to only carry one type of fruit each.

What is the total amount of fruit you can collect with this procedure?

Example 1:

Input: [1,2,1]
Output: 3
Explanation: We can collect [1,2,1].
Example 2:

Input: [0,1,2,2]
Output: 3
Explanation: We can collect [1,2,2].
If we started at the first tree, we would only collect [0, 1].
Example 3:

Input: [1,2,3,2,2]
Output: 4
Explanation: We can collect [2,3,2,2].
If we started at the first tree, we would only collect [1, 2].
Example 4:

Input: [3,3,3,1,2,1,1,2,3,3,4]
Output: 5
Explanation: We can collect [1,2,1,1,2].
If we started at the first tree or the eighth tree, we would only collect 4 fruits.
Note:

1 <= tree.length <= 40000
0 <= tree[i] < tree.length
解题思路
问题类似于在一个字符串里找最长子序列，满足要求（包含的数的类型不超过两个）的最长子序列；

考虑一种类似滑动窗口的实现方式，首先，定义一个Map，存储出现过的数的类型（Key），Value是这个数在当前窗口里出现过的次数；

首先把滑动窗口的左边放到开头的位置，然后一步一步地向后走，遇到新的数，即Map里没有的，就添加到Map里；

当这个Map里存的Key超过两个的时候，开始移动滑动窗口的左边，一步删掉一个数，当这个数在滑动窗口里出现的次数变成0的时候，可以把这个数从Map里移除了；

一直控制这个Map维持两个的大小，超过两个就移动窗口的左边，一直走到头，不断比较窗口的大小，留下一个最大值，即是解；

class Solution {
     public int totalFruit(int[] tree) {
        int res = 0;
        if (tree == null || tree.length < 1) {
            return res;
        }
        if (tree.length < 3) {
            return tree.length;
        }
        Map<Integer,Integer> container = new HashMap<>();
        int i = 0; // left pointer
        int cur = 1;
        container.put(tree[0],1);
        for (int k = 1; k < tree.length; k++) {
            cur ++;
           /* if (container.containsKey(tree[k])) {
                Integer t = container.get(tree[k]);
                t += 1;
                container.put(tree[k],t);
            } else {
                container.put(tree[k],1);
            }*/
           container.put(tree[k],container.getOrDefault(tree[k],0) + 1);
            // left pointer go
            
            while (container.size() > 2) {
                container.put(tree[i],container.get(tree[i]) - 1);
                if (container.get(tree[i]) == 0) {
                    container.remove(tree[i]);
                }
                i++;
                cur--;
            }
            res = Math.max(cur,res);

        }
        return res;
    }
}