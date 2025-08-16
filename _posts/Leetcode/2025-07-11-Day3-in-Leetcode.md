---
title: Day3 in Leetcode
date: 2025-07-11
categories: [Leetcode]
tags: [Leetcode, Algorithm]
---

# 203. 移除链表元素
使用虚拟头结点，遍历链表，遇到等于 val 的节点就删除。

# 707. 设计链表
用带虚拟头结点的单链表实现，要注意边界条件。

# 206. 反转链表
**一句话思路**：用三个指针（prev、curr、next）迭代反转每个节点的指向
**模板**：
ListNode* prev = nullptr;
ListNode* curr = head;
while (curr) {
    ListNode* next = curr->next;
    curr->next = prev;
    prev = curr;
    curr = next;
}
return prev;
**易错**：返回的是prev不是curr
**类似题**：
24.两两交换链表中的节点
19.删除链表的倒数第N个节点
142.环形链表II
203.移除链表元素