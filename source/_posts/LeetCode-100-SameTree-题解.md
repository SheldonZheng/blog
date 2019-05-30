---
title: LeetCode.100.SameTree 题解
tags:
  - LeetCode 题解
  - 二叉树
  - 算法
date: 2016-08-16 10:15:29
---

[原题地址](https://leetcode.com/problems/same-tree/)

题目描述：

Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

&nbsp;

给出两个二叉树，判断是否相等；相等的定义是有相同的结构，且有相同的值；

&nbsp;

&nbsp;

这里有两种写法，一是判断为空的情况和所有不是相等二叉树的情况，最后递归地判断下去；二是直接判断这个二叉树是不是相等，然后递归地判断下去；第二种方法更加简洁。第一种方法的实现写在了注释里；

<pre>public class SameTree {

    public boolean isSameTree(TreeNode p, TreeNode q) {

        return (p == null &amp;&amp; q == null) || ((p != null &amp;&amp;q != null &amp;&amp; p.val == q.val) &amp;&amp; (isSameTree(p.left,q.left) &amp;&amp; isSameTree(p.right,q.right)));

       /* if(p == null &amp;&amp; q == null)
            return true;

        else if(p == null &amp;&amp; q != null)
            return false;

        else if(p != null &amp;&amp; q == null)
            return false;

        else if(p != null &amp;&amp; q != null &amp;&amp; p.val != q.val)
            return false;

        else
            return (isSameTree(p.left,q.left) &amp;&amp; isSameTree(p.right,q.right));*/
    }

    private class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int x) { val = x; }
    }

}</pre>