---
title: Day1 in Leetcode
date: 2025-07-09
categories: [Leetcode]
tags: [Leetcode, Algorithm]
---

## 704. 二分查找
**一句话思路**：在有序数组中，每次排除一半的搜索空间，直到找到目标值
**模板**：
int left = 0, right = nums.size() - 1;
while (left <= right) {
    int mid = left + (right - left) / 2;
    nums[mid] == target ? return mid : ;
    nums[mid] < target ? left = mid + 1 : ;
    nums[mid] > target ? left = mid - 1 : ;
}
return -1;
**易错**：循环条件是 <= 不是 <（因为right初始值是size-1）
**类似题**：
27.移除元素 - 虽然不是二分，但也是双指针在数组中查找
209.长度最小的子数组 - 滑动窗口本质也是缩小搜索范围

# 27. 移除元素
**一句话思路**：快慢指针，快指针遍历，慢指针记录有效位置
**模板**：
int slow = 0;
for (int fast = 0; fast < nums.size(); fast++) {
    if (nums[fast] != val)
        nums[slow++] = nums[fast];
}
return slow;
**易错**：不需要真正删除元素，只需要覆盖
**类似题**：暂无

# 977. 有序数组的平方
**一句话思路**：
**模板**：
for (int i = 0; i < nums.size(); i++) {
    int a = nums[i];
    int aa = a * a;
    nums[i] = aa;
}
sort(nums.begin(), nums.end());
return nums;
**易错**：也可以用左右指针
**类似题**：暂无
