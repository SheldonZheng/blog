---
title: LeetCode.155.MinStack最小栈题解
date: 2019-05-15 17:55:49
tags:
---

题目地址

原题:
​ 155. Min Stack(最小栈)

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) – Push element x onto stack.
pop() – Removes the element on top of the stack.
top() – Get the top element.
getMin() – Retrieve the minimum element in the stack.
Example:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
###解题思路:

​ 使用一个可变数组，一个指针指向当前栈顶，一个数存当前最小值；

每次push新数值的时候，比较最小值，看看是否要更新最小值；

每次pop数值的时候，如果pop的是最小值，需要从剩下的数里重新选出一个最小值；

这里可能比较浪费性能，因为是一次全部扫描；

有种思路是存双倍的数，push一个数的时候，先判断这个数是不是要替换之前的那个最小数，如果是，就先把之前的最小数放到栈顶的下面，pop的时候，如果pop了栈顶(新的最小数没了)，就再pop一次，拿之前的那个最小数顶，我的代码里没有实现；

附上题解

class MinStack {

        private List<Integer> container;

        private int p;

        private int min;

        /** initialize your data structure here. */
        public MinStack() {
            container = new ArrayList<>();
            p = 0;
            min = Integer.MAX_VALUE;
        }

        public void push(int x) {
            container.add(p,x);
            min = Math.min(min,x);
            p++;
        }

        public void pop() {
            if (p >= 1) {
                if (container.get(p - 1) != null && container.get(p - 1) == min) {
                    container.add(p - 1, null);

                    min = Integer.MAX_VALUE;
                    for (int i = 0; i < p - 1; i++) {
                        Integer integer = container.get(i);
                        if (integer != null) {
                            min = Math.min(integer,min);
                        }
                    }

                } else {
                    container.add(p - 1, null);

                }
            }
            if (p >= 1) {
                p--;
            }
        }

        public int top() {
            if (p >= 1) {
                return container.get(p - 1);
            } else {
                return -1;
            }
        }

        public int getMin() {
            return min;
        }
}
