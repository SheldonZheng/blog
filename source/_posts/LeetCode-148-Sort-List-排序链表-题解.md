---
title: LeetCode 148 Sort List 排序链表 题解
date: 2019-05-15 17:20:04
tags:
---

题目地址

Description:
Sort a linked list in O(n log n) time using constant space complexity.

Example 1:

Input: 4->2->1->3
Output: 1->2->3->4
Example 2:

Input: -1->5->3->4->0
Output: -1->0->3->4->5
题解:
要求对一个链表进行排序，时间复杂度要求O(n log n)，占用常数级空间。

简单一想，可以把链表里所有的数抽出来放到数组里然后排序，然后重构链表；

或者直接对链表进行归并排序，但是怎么取中位数呢？

​ 使用两个指针，一个一次走两步，一个一次走一步，快的那个走到头了，慢的那个就走到中间了；

然后归并起来就可以了；

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
     public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode fast = head,slow = head;

        //cut link
        ListNode cut = null;

        while (fast != null && fast.next != null) {
            cut = slow;
            slow = slow.next;
            fast = fast.next.next;
        }

        //cut link
        cut.next = null;
        

        return mergeTwoListNode(sortList(head),sortList(slow));
    }

    public ListNode mergeTwoListNode(ListNode o ,ListNode t) {
        ListNode c = new ListNode(-1);
        ListNode p = c;

        while (o != null && t != null) {
            if (o.val < t.val) {
                p.next = o;
                o = o.next;
            } else {
                p.next = t;
                t = t.next;
            }
            p = p.next;
        }

        if (o != null) {
            p.next = o;
        }
        if (t != null) {
            p.next = t;
        }

        return c.next;
    }
}
