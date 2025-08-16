---
title: Day4 in Leetcode
date: 2025-07-12
categories: [Leetcode]
tags: [Leetcode, Algorithm]
---

# 24. 两两交换链表中的节点
用虚拟头结点，遍历链表，每次交换一对节点。

# 19. 删除链表的倒数第N个节点
**一句话思路**：用快慢指针，快指针先走 n 步，然后快慢一起走，快指针到末尾时慢指针正好在待删除节点的前一个。
**模板**：
ListNode* dummy = new ListNode(0);
dummy->next = head;
ListNode* fast = dummy;
ListNode* slow = dummy;

for (int i = 0; i <= n; i++) {
    fast = fast->next;
}

while (fast) {
    fast = fast->next;
    slow = slow->next;
}

slow->next = slow->next->next;
return dummy->next;
**易错**：必须用dummy节点处理删除头节点的情况
**类似题**：
142.环形链表II
203.移除链表元素
206.反转链表
24.两两交换链表中的节点

# 面试题 02.07. 链表相交
双指针分别遍历两个链表，走到末尾后切换到另一个链表头，最终会在交点相遇或都为 None。

# 142. 环形链表 II
**一句话思路**：快慢指针找相遇点，然后一个从头、一个从相遇点同速走，再次相遇即环入口
**模板**：
设：a = 起点到环入口的距离
    b = 环入口到相遇点的距离
    c = 环的长度

相遇时：
- slow走了：a + b
- fast走了：a + b + n*c（多走了n圈）
- fast是slow的2倍速

所以：2(a + b) = a + b + n*c
     => a + b = n*c
     => a = n*c - b
     => a = (n-1)*c + (c-b)

这意味着：
从head走a步 = 从相遇点走(c-b)步，都会到达环入口

ListNode *fast = head, *slow = head;
while (fast && fast->next) {
    fast = fast->next->next;
    slow = slow->next;
    if (fast == slow) break;
}
if (!fast || !fast->next) return nullptr;

ListNode *p1 = head, *p2 = slow;
while (p1 != p2) {
    p1 = p1->next;
    p2 = p2->next;
}
return p1;
**易错**：数学原理
**类似题**：
141.环形链表
202.快乐数
19.删除链表的倒数第N个节点
206.反转链表
