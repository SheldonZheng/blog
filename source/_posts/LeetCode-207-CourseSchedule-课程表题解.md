---
title: LeetCode.207.CourseSchedule.课程表题解
date: 2019-05-15 17:55:12
tags:
---

题目地址

207.Course Schedule

There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

Example 1:

Input: 2, [[1,0]] 
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
Example 2:

Input: 2, [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
Note:

The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
You may assume that there are no duplicate edges in the input prerequisites.
解题思路
首先，我们要解决的是一个什么样的问题？

题目里给出了提示，就是判断一个图，是不是有向无环图(DAG)，即图中不存在环；

首先定义一个数组，用来标识某个数的访问状态(未访问(0)、访问中(-1)、已访问完成(1))；

然后定义一个Map，key为某个数，value是一个数组，数组里包含要到达这个数(key)要访问的前置节点；

然后从0开始(因为题目中写了(0…n-1))，遍历这个数，判断这个数的前置节点，是否已经被访问过了；

代码:
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (numCourses == 0 || prerequisites == null) {
            return false;
        }

        int []vis = new int[numCourses];

        //初始化 存放 前置条件的地方
        //将访问某个数的先决条件放到这里来
        Map<Integer,ArrayList<Integer>> container = new HashMap<>();
        for (int i = 0; i < prerequisites.length; i++) {
            if (container.containsKey(prerequisites[i][1])) {
                container.get(prerequisites[i][1]).add(prerequisites[i][0]);
            } else {
                ArrayList<Integer> t = new ArrayList<>();
                t.add(prerequisites[i][0]);
                container.put(prerequisites[i][1],t);
            }
        }

        for (int i = 0; i < numCourses; i++) {
            //如果访问某个数的时候，发现它的先决条件已经被访问过了 就是有环
            if (!dfs(container,vis,i)) {
                return false;
            }
        }
        return true;

    }

    private boolean dfs(Map<Integer,ArrayList<Integer>> container,int []vis ,int i) {
        //还没访问结束
        if (vis[i] == -1) {
            return false;
        }
        //访问结束
        if (vis[i] == 1) {
            return true;
        }

        //开始访问 (进入递归链)
        vis[i] = -1;
        //如果有值没有任何先决条件，就不会走到这里的if里面
        if (container.containsKey(i)) {
            ArrayList<Integer> t = container.get(i);
            for (Integer integer : t) {
                if (!dfs(container,vis,integer)) {
                    return false;
                }
            }
        }

        //访问结束
        vis[i] = 1;
        return true;
    }
}