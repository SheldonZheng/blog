---
title: LeetCode.103.Binary Tree Zigzag Level Order Traversal 题解
tags:
  - LeetCode 题解
  - 二叉树
  - 算法
date: 2016-08-19 10:49:55
---

[原题地址](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

&nbsp;

题目描述：Given a binary tree, return the _zigzag level order_ traversal of its nodes&#8217; values. (ie, from left to right, then right to left for the next level and alternate between).

&nbsp;

给入一个二叉树，通过Zig-Zag遍历返回一个二层的List；

思路是构造一个队列，先放入root节点，第一次遍历把root节点的左右节点放进去，下一次遍历就是root节点的左右节点的子节点……依次类推；

因为是Zig-Zag遍历，所以放置一个flag来判断是不是要翻转结果；

注意开头的root==null的判断；

<pre>public class BinaryTreeZigzagLevelOrderTraversal {

    public List&lt;List&lt;Integer&gt;&gt; zigzagLevelOrder(TreeNode root) {
        List&lt;List&lt;Integer&gt;&gt; result = new ArrayList&lt;&gt;();
        int flag = -1;
        if(root == null)
            return result;

        Queue&lt;TreeNode&gt; queue = new LinkedList&lt;&gt;();
        queue.add(root);

        while(queue.peek() != null)
        {
            flag = 0 - flag;
            int size = queue.size();
            List&lt;Integer&gt; list = new ArrayList&lt;&gt;();
            for (int i = 0;i &lt; size;i++)
            {
                TreeNode p = queue.poll();
                list.add(p.val);
                if(p.left != null)
                    queue.add(p.left);
                if(p.right != null)
                    queue.add(p.right);
            }
            if(flag == -1)
                Collections.reverse(list);
            result.add(list);
        }
        return result;
    }

    private class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int x) { val = x; }
    }

}</pre>