---
title: Day9 in Leetcode
date: 2025-07-17
categories: [Leetcode]
tags: [Leetcode, Algorithm]
---

# 151. 翻转字符串里的单词
**一句话思路**：三步走 - 去多余空格 → 整体反转 → 每个单词反转
**例子解析**：
        int slow = 0;
        for (int fast = 0; fast < s.size(); fast++) {
            if (s[fast] != ' ') {
                if (slow != 0)
                    s[slow++] = ' ';
                while (fast < s.size() && s[fast] != ' ') {
                    s[slow++] = s[fast++];
                }
            }
        }
        s.resize(slow);
        reverse(s.begin(), s.end());
        int start = 0;
        for (int i = 0; i <= s.size(); i++) {
            if (i == s.size() || s[i] == ' ') {
                reverse(s.begin() + start, s.begin() + i);
                start = i + 1;
            }
        }
        return s;
**易错**：第一步去空格时，要确保单词间只有一个空格，且首尾无空格
**类似题**：
344.反转字符串 - 基础的反转操作
541.反转字符串II - 分段反转思想

# 28. 实现 strStr()
**一句话思路**：KMP算法，构建next数组进行匹配，避免重复比较
**模板**：
        int n = haystack.size(), m = needle.size();
        for (int i = 0; i + m <= n; i++) {
            bool flag = true;
            for (int j = 0; j < m; j++) {
                if (haystack[i + j] != needle[j]) {
                    flag = false;
                    break;
                }
            }
            if (flag) {
                return i;
            }
        }
        return -1;
**易错**：next数组的构建逻辑，以及匹配失败时的回退位置
**类似题**：
459.重复的子字符串 - 也可以用KMP的next数组来解决
214.最短回文串 - KMP的应用变种

# 459. 重复的子字符串
**一句话思路**：如果字符串由重复子串构成，那么s+s去掉首尾字符后，原字符串s应该在其中
**模板**：
        string doubled = s + s;
        return doubled.substr(1, doubled.size() - 2).find(s) != string::npos;
**易错**：要去掉首尾各一个字符，避免匹配到原位置
**类似题**：
28.实现strStr() - 字符串匹配的基础
686.重复叠加字符串匹配 - 类似的重复字符串问题 