---
title: LeetCode.33.SearchInRotatedSortedArray题解
date: 2019-06-17 16:41:29
categories: 
- LeetCode题解
tags: 
- LeetCode
---

[原题地址](https://leetcode.com/problems/search-in-rotated-sorted-array/)

### Description:

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`).

You are given a target value to search. If found in the array return its index, otherwise return `-1`.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```



### 题解:

本质还是二分查找，只不过多了一个旋转点；

所以每次二分的时候要判断是不是有序的，因为是升序排列，判断左半边是否有序，即nums[mid] > nums[start]成立吗，成立就是左半边有序，反之右半边有序；

左半边有序就先判断左边的边界，如果不满足就抛弃左边，进行下一次二分；

右边同理；



### Code:

```java
public class Solution {
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
        while (start + 1 < end) {
            mid = start + (end - start) /2;
            if (nums[mid] == target)
                return mid;
            else if (nums[mid] > nums[start]) {
                if (target >= nums[start] && target <= nums[mid])
                    end = mid;
                else {
                    start = mid;
                }
            }
            else {
                if (target >= nums[mid] && target <= nums[end]) {
                    start = mid;
                }
                else {
                    end = mid;
                }
            }
        }

        return -1;
    }
}
```

