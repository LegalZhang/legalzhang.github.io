---
title: Day2 in Leetcode
date: 2025-07-10
categories: [Leetcode]
tags: [Leetcode, Algorithm]
---

# 209. 长度最小的子数组
使用滑动窗口法。用两个指针维护一个窗口，右指针不断向右扩展，直到窗口内的和大于等于target，然后尝试收缩左指针以找到最小长度。

# 59. 螺旋矩阵 II
按层模拟螺旋填充，每次循环填充矩阵的上、右、下、左四条边。