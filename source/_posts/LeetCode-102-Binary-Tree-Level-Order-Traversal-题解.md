---
title: LeetCode.102.Binary Tree Level Order Traversal 题解
tags:
  - LeetCode 题解
  - 二叉树
  - 算法
date: 2016-08-19 10:48:39
---

[原题地址](https://leetcode.com/problems/binary-tree-level-order-traversal/)

&nbsp;

题目描述：Given a binary tree, return the _level order_ traversal of its nodes&#8217; values. (ie, from left to right, level by level).

很简单的层级顺序遍历，思路是构造一个队列，先放入root节点，

第一次遍历把root节点的左右节点放进去，下一次遍历就是root节点的左右节点的子节点……依次类推。

<pre>
public class BinaryTreeLevelOrderTraversal {

    public List&lt;List&lt;Integer&gt;&gt; levelOrder(TreeNode root) {
        List&lt;List&lt;Integer&gt;&gt; result = new ArrayList&lt;&gt;();
        if(root == null)
            return result;

        Queue&lt;TreeNode&gt; queue = new LinkedList&lt;&gt;();
        queue.add(root);

        while(queue.peek() != null)
        {
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

&nbsp;