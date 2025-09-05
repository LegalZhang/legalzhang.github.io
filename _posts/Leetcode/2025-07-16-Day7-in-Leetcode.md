---
title: Day7 in Leetcode
date: 2025-07-15
categories: [Leetcode]
tags: [Leetcode, Algorithm]
---

# 454. 四数相加II
**一句话思路**：用哈希表记录前两个数组的和，然后遍历后两个数组，查找是否有相反数
**模板**：
        unordered_map<int, int> umap;
        for (int a : nums1) {
            for (int b : nums2) {
                umap[a + b]++;
            }
        }
        int count = 0;
        for (int c : nums3) {
            for (int d : nums4) {
                if (umap.find(0 - (c + d)) != umap.end()) {
                    count += umap[0 - (c + d)];
                }
            }
        }
        return count;
**易错**：要累加map[target]的值，因为可能有多种组合
**类似题**：
1.两数之和 - 哈希表查找配对
15.三数之和 - 多数之和问题的基础

# 383. 赎金信
**一句话思路**：用哈希表统计magazine中每个字符的出现次数，然后遍历ransomNote检查是否足够
**模板**：
        int record[26] = {0};
        if (ransomNote.size() > magazine.size()) {
            return false;
        }
        for (int i = 0; i < magazine.length(); i++) {
            record[magazine[i] - 'a'] ++;
        }
        for (int j = 0; j < ransomNote.length(); j++) {
            record[ransomNote[j] - 'a'] --;
            if(record[ransomNote[j] - 'a'] < 0) {
                return false;
            }
        }
        return true;
**易错**：也可以用unordered_map，但数组更高效
**类似题**：
242.有效的字母异位词 - 同样是字符频次统计
349.两个数组的交集 - 哈希表查找

# 15. 三数之和
**一句话思路**：排序后固定一个数，用双指针在剩余数组中找两数之和等于目标值
**模板**：
        vector<vector<int>> result;
        sort(nums.begin(), nums.end());

        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] > 0)
                break;
            
            if (i > 0 && nums[i] == nums[i - 1])
                continue;

            unordered_set<int> set;

            for (int k = i + 1; k < nums.size(); k++) {
                if (k > i + 2 && nums[k] == nums[k - 1] && nums[k - 1] == nums[k - 2])
                    continue;

                int target = 0 - (nums[i] + nums[k]);
                if (set.find(target) != set.end()) {
                    result.push_back({nums[i], target, nums[k]});
                    set.erase(target);
                }
                else {
                    set.insert(nums[k]);
                }
            }
        }
        return result;
**易错**：三个地方都要去重：i的去重，left的去重，right的去重
**类似题**：
1.两数之和 - 基础问题
18.四数之和 - 扩展问题
454.四数相加II - 不同的解法思路

# 18. 四数之和
**一句话思路**：类似三数之和，多一层循环固定第二个数，注意去重和剪枝优化
**模板**：
        vector<vector<int>> result;
        sort(nums.begin(), nums.end());
        for (int k = 0; k < nums.size(); k++) {
            if (nums[k] > target && nums[k] >= 0) {
                break;
            }

            if(k > 0 && nums[k] == nums[k - 1]) {
                continue;
            }

            for (int i = k + 1; i < nums.size(); i++) {
                if (nums[k] + nums[i] > target && nums[k] + nums[i] >= 0) {
                    break;
                }

                if (i > k + 1 && nums[i] == nums[i - 1]) {
                    continue;
                }
                int left = i + 1;
                int right = nums.size() - 1;
                while (right > left) {
                    if ((long) nums[k] + nums[i] + nums[left] + nums[right] > target) {
                        right--;
                    } else if ((long) nums[k] + nums[i] + nums[left] + nums[right] < target) {
                        left++;
                    } else {
                        result.push_back(vector<int>{nums[k], nums[i], nums[left], nums[right]});
                        while (right > left && nums[right] == nums[right - 1]) right--;
                        while (right > left && nums[left] == nums[left + 1]) left++;

                        right--;
                        left++;
                    }
                }
            }
        }
        return result;
**易错**：注意数据溢出，使用long long；四个地方都要去重
**类似题**：
15.三数之和 - 基础模板
1.两数之和 - 最基础问题
454.四数相加II - 不同解法 