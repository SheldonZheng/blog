---
title: LeetCode.108.Convert Sorted Array to Binary Search Tree 题解
tags:
  - LeetCode 题解
  - 二叉树
  - 算法
date: 2016-08-17 11:06:23
---

[原题地址](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

题目描述：Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

给入一个排序好的数组，返回一个用它构建出来的BST（Binary Search Tree）二叉排序树；

&nbsp;

解题思路：既然是已经排好序的数组，排序我们就不用关心。采用二分的方法求解：首先找到中点，然后中点构建一个root节点，左边所有的值递归构建二叉树，右边也是如此。这样有两种边界条件：

1.当array.size() = 0的时候，直接返回null;

2.当array.size() = 2的时候，即只有array[0],array[1]有值的时候，我们只能构建中间的root节点和右边的一个子节点；

判断这两种边界条件即可；

&nbsp;

<pre>
public class ConvertSortedArrayToBST {

    public TreeNode sortedArrayToBST(int[] nums) {

        return sortedArrayToBST(nums,0,nums.length - 1);
    }

    private TreeNode sortedArrayToBST(int[] nums,int start,int end)
    {
        if(start &gt; end)
            return null;

        int mid = (start + end) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        if(start == end)
            return root;

        root.left = sortedArrayToBST(nums,start,mid - 1);
        root.right = sortedArrayToBST(nums,mid + 1,end);

        return root;

    }

    private class TreeNode {
             int val;
             TreeNode left;
             TreeNode right;
             TreeNode(int x) { val = x; }
    }
}</pre>