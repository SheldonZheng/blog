---
title: LeetCode.110.Balanced Binary Tree 题解
tags:
  - LeetCode 题解
  - 二叉树
  - 算法
date: 2016-08-11 16:32:29
---

[原题地址](https://leetcode.com/problems/balanced-binary-tree/)

题目描述：

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of _every_ node never differ by more than 1.

给入一个二叉树，判断这个二叉树是不是平衡二叉树，返回true或者false。我在做这道题的时候只看了第一行，没看下面关于平衡二叉树的定义。走了一点弯路。我起初认为平衡二叉树是要求如果左节点不为空那么右节点也不能为空，反之也如此。其实平衡二叉树的定义是两个子节点的高度差不能大于一。那么我们就要实现一个计算二叉树深度的函数，然后比较结果就好了。代码如下：

&nbsp;

<pre>public class BalancedBinaryTree {

    public boolean isBalanced(TreeNode root) {

        if(root == null)
            return true;

        int leftCount = maxDepth(root.left);
        int rightCount = maxDepth(root.right);

        if(leftCount &gt; rightCount + 1 || rightCount &gt; leftCount + 1)
            return false;

        return (isBalanced(root.left) &amp;&amp; isBalanced(root.right));
    }

    public int maxDepth(TreeNode root)
    {
        if(root == null)
            return 0;

        int leftCount = maxDepth(root.left);
        int rightCount = maxDepth(root.right);

        return leftCount &gt; rightCount ? leftCount + 1 : rightCount + 1;

    }

    public class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int x) { val = x; }
    }

}</pre>