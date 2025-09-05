---
title: Day6 in Leetcode
date: 2025-07-14
categories: [Leetcode]
tags: [Leetcode, Algorithm]
---

# 242. 有效的字母异位词
**一句话思路**：先判断长度，然后对两个字符串排序，排序后相等则为字母异位词
**模板**：
    bool isAnagram(string s, string t) {
        if (s.length() != t.length()) {
            return false;
        }
        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
        return s == t;
    }
**易错**：也可以用哈希表统计字符频次，时间复杂度O(n)更优于排序的O(nlogn)
**类似题**：
349.两个数组的交集 - 同样使用哈希思想
1.两数之和 - 哈希表的经典应用

# 349. 两个数组的交集
**一句话思路**：先把一个集合放到hash set中，然后求另一个数组与其的交集
**模板**：
        unordered_set<int> result_set;
        unordered_set<int> nums_set(nums1.begin(), nums1.end());
        for (int num : nums2) {
            if (nums_set.find(num) != nums_set.end()) {
                result_set.insert(num);
            }
        }
        return vector<int>(result_set.begin(), result_set.end());
**易错**：结果不需要去重，因为用的是set
**类似题**：
350.两个数组的交集II - 需要考虑重复元素
242.有效的字母异位词 - 同样是哈希统计

# 202. 快乐数
**一句话思路**：用哈希集合记录出现过的数字，若出现循环则不是快乐数，若到1则是快乐数
**模板**：
    int getSum(int n) {
        int sum = 0;
        while (n) {
            sum += (n % 10) * (n %10);
            n /= 10;
        }
        return sum;
    }
    bool isHappy(int n) {
        unordered_set<int> set;
        while(1) {
            int sum = getSum(n);
            if (sum == 1) {
                return true;
            }
            if (set.find(sum) != set.end()) {
                return false;
            } else {
                set.insert(sum);
            }
            n = sum;
        }
    }
return n == 1;
**易错**：也可以用快慢指针检测循环（类似链表环检测）
**类似题**：
142.环形链表II - 循环检测的思想相同
1.两数之和 - 哈希表记录已访问元素

# 1. 两数之和
**一句话思路**：用哈希表记录已访问的数字及其下标，边遍历边查找target-当前值
**模板**：
        unordered_map<int, int> map;
        for (int i = 0; i < nums.size(); i++) {
            int other = target - nums[i];
            if (map.find(other) != map.end()) {
                return {map[other], i};
            }
            map[nums[i]] = i;
        }
        return {};
**易错**：要先查找再插入，避免使用同一个元素两次
**类似题**：
15.三数之和 - 多数之和问题的基础
242.有效的字母异位词 - 哈希表统计
349.两个数组的交集 - 哈希表查找