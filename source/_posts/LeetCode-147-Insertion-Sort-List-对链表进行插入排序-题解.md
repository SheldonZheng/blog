---
title: LeetCode 147 Insertion Sort List 对链表进行插入排序 题解
date: 2019-05-15 17:17:58
tags:
---

题目地址

Description:
Sort a linked list using insertion sort.

img
A graphical example of insertion sort. The partial sorted list (black) initially contains only the first element in the list.
With each iteration one element (red) is removed from the input data and inserted in-place into the sorted list

Algorithm of Insertion Sort:

Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.
At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.
It repeats until no input elements remain.
Example 1:

Input: 4->2->1->3
Output: 1->2->3->4
Example 2:

Input: -1->5->3->4->0
Output: -1->0->3->4->5
题解：
定义一个前置节点，next = head，这样可以处理往前插入的情况；

从前向后扫描，遇到不符合顺序的数据，寻找它应该在的位置，截断链表插入；

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode c = new ListNode(-1);
        c.next = head;
        ListNode p = head;
        while (p.next != null) {
            if (p.next.val >= p.val) {
                p = p.next;
            } else {
               ListNode t = p.next;
               ListNode f = c;
               //cut
               p.next = p.next.next;
               //find
               while (f.next.val < t.val) {
                   f = f.next;
               }
               //link
                t.next = f.next;
                f.next = t;
            }

        }
        return c.next;
    }
}