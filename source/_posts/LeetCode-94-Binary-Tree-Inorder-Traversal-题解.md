---
title: LeetCode.94.Binary Tree Inorder Traversal 题解
tags:
  - LeetCode 题解
  - 二叉树
  - 算法
date: 2016-08-18 10:55:47
---

[原题地址](https://leetcode.com/problems/binary-tree-inorder-traversal/)

题目描述：Given a binary tree, return the _inorder_ traversal of its nodes&#8217; values.

&nbsp;

简单来说就是一个二叉树的中序遍历。题目下面有Note，要求不要采用递归的解法。这里递归的解法是最容易理解的，但是一方面是慢，另一方面是要占用大量的空间，容易爆栈。这里采用循环的方式解；

构建一个指针p，如果p不为空，那么将p入栈，p指向p的左节点；

如果p为空，说明已经走到尽头了，那么将栈顶弹出，加入结果集，并且访问右节点；

代码：

<pre>public List&lt;Integer&gt; inorderTraversal(TreeNode root) {

    List&lt;Integer&gt; result = new ArrayList&lt;&gt;();

    Stack&lt;TreeNode&gt; stk = new Stack&lt;&gt;();

    TreeNode p = root;

    while (p != null || !stk.empty())
    {
        if(p != null)
        {
            stk.push(p);
            p = p.left;
        }
        else
        {
            p = stk.pop();
            result.add(p.val);
            p = p.right;
        }
    }

    return result;
}

private class TreeNode {
         int val;
         TreeNode left;
         TreeNode right;
         TreeNode(int x) { val = x; }
}</pre>