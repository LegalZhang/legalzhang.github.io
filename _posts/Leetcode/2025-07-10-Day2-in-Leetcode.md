---
title: Day2 in Leetcode
date: 2025-07-10
categories: [Leetcode]
tags: [Leetcode, Algorithm]
---

# 209. 长度最小的子数组
**一句话思路**：滑动窗口维护和>=target的最小区间
**模板**：
int left = 0, sum = 0, minLen = INT_MAX;
for (int right = 0; right < nums.size(); right++) {
    sum += nums[right];
    while (sum >= target) {
        minLen = min(minLen, right - left + 1);
        sum -= nums[left++];
    }
}
return minLen == INT_MAX ? 0 : minLen;
**易错**：初始化minLen为INT_MAX（任意大于数组size的数），最后要判断是否更新过
**类似题**：
704.二分查找 - 前缀和解法需要二分
239.滑动窗口最大值 - 同样是滑动窗口思想
15.三数之和 - 双指针移动思想类似

# 59. 螺旋矩阵 II
**一句话思路**：按照右、下、左、上的顺序，一圈圈从外向内填充数字
**模板**：
vector<vector<int>> matrix(n, vector<int>(n));
int left = 0, right = n - 1, top = 0, bottom = n - 1;
int num = 1;
while (left <= right && top <= bottom) {
    for (int i = left; i <= right; i++) matrix[top][i] = num++;
    top++;
    for (int i = top; i <= bottom; i++) matrix[i][right] = num++;
    right--;
    for (int i = right; i >= left; i--) matrix[bottom][i] = num++;
    bottom--;
    for (int i = bottom; i >= top; i--) matrix[i][left] = num++;
    left++;
}
return matrix;
**易错**：边界控制：每条边的起止位置容易重复或遗漏
**类似题**：暂无
