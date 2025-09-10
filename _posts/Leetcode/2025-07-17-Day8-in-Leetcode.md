---
title: Day8 in Leetcode
date: 2025-07-16
categories: [Leetcode]
tags: [Leetcode, Algorithm]
---

# 344. 反转字符串
**一句话思路**：双指针从两端向中间移动，交换字符
**模板**：
        int left = 0, right = s.size() - 1;
        while (left < right) {
            swap(s[left], s[right]);
            left++;
            right--;
        }
**易错**：条件是left < right，不是left <= right
**类似题**：
541.反转字符串II - 分段反转的变种
151.翻转字符串里的单词 - 也需要反转操作

# 541. 反转字符串II
**一句话思路**：每2k个字符为一组，反转前k个字符
**模板**：
        for (int i = 0; i < s.size(); i += 2 * k) {
            if (i + k <= s.size()) {
                reverse(s.begin() + i, s.begin() + i + k);
            } else {
                reverse(s.begin() +i, s.end());
            }
        }
        return s;
**易错**：要考虑剩余字符数不足k的情况，需要全部反转
**类似题**：
344.反转字符串 - 基础的反转操作
151.翻转字符串里的单词 - 更复杂的分段反转 