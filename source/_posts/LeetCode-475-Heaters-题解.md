---
title: LeetCode.475 Heaters 题解
tags:
  - LeetCode 题解
date: 2018-10-17 11:27:26
---

LeetCode.475 Heaters 题解

[题目地址](https://leetcode.com/problems/heaters/description/)

解题思路：

第一步先找到所有房屋距离自己最近的供暖器的距离；

第二步找到一个最大值，大于或等于所有房屋距离自己最近的供暖器的距离（其实就是某个房屋离供暖器的位置最远）

这两步可以结合在一起，迭代来更新最终值

&nbsp;

<pre>public int findRadius(int[] houses, int[] heaters) {
if (houses == null || heaters == null) {
return 0;
}
Arrays.sort(houses);
Arrays.sort(heaters);

int r = 0;
int j = 0;
for (int house : houses) {
while (j &lt; heaters.length - 1 &amp;&amp; Math.abs(heaters[j] - house) &gt;= Math.abs(heaters[j + 1] - house)) {
j++;
}
r = Math.max(r,Math.abs(heaters[j] - house));
}
return r;

}</pre>