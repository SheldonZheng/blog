---
title: LeetCode.33.Search in Rotated Sorted Array题解
tags:
  - LeetCode 题解
  - 算法
date: 2017-05-08 15:53:15
---

## LeetCode.33.Search in Rotated Sorted Array题解

[原题地址](https://leetcode.com/problems/search-in-rotated-sorted-array/#/description)

假设有一个排序的按未知的旋转轴旋转的数组(比如，0 1 2 4 5 6 7 可能成为4 5 6 7 0 1 2)。给定一个目标值进行搜索，如果在数组中找到目标值返回数组中的索引位置，否则返回-1。

&nbsp;

解法很简单 就像二分查找一样 但是因为这个数组是旋转过的 所以要特殊判断一下当前mid的命中位置是不是旋转过的位置，别的处理跟二分查找一样 要注意数组只有一个元素和两个元素的特殊情况处理；

<pre>public class SearchInRotatedSortedArray {

    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0)
            return -1;

        int start = 0;
        int end = nums.length - 1;
        int mid = 0;
        if(nums[start] == target)
            return start;
        if(nums[end] == target)
            return end;
        while (start + 1 &lt; end) { mid = start + (end - start) /2; if (nums[mid] == target) return mid; else if (nums[mid] &gt; nums[start]) {
                if (target &gt;= nums[start] &amp;&amp; target &lt;= nums[mid]) end = mid; else { start = mid; } } else { if (target &gt;= nums[mid] &amp;&amp; target &lt;= nums[end]) {
                    start = mid;
                }
                else {
                    end = mid;
                }
            }
        }

        return -1;
    }
}</pre>