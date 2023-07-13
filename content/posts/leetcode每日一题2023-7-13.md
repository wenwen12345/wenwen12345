---
title: "Leetcode每日一题2023 7 13"
date: 2023-07-13T15:08:30+08:00
categories:
tags:
draft: true
---

# leetcode 每日一题

今天的[每日一题](https://leetcode.cn/problems/minimum-falling-path-sum/)是一道动态规划的题目，难度中等。

## 思路

使用动态规划，定义`dp[i][j]`为从最高点走到当前点的最小数字和，最顶端的数为 matrix 中的对应数字，每一个点都可以从他的左上、右上和上方转移，除非没有值。最后返回最后一列中的最小值

## 实现

```cpp
class Solution {
public:
  int minFallingPathSum(vector<vector<int>> &matrix) {
    vector<vector<int>> dp(matrix.size(), vector<int>(matrix[0].size()));
    dp[0] = matrix[0];
    for (int i = 1; i < matrix.size(); i++) {
      for (int j = 0; j < matrix[i].size(); j++) {
        vector<int> cmp{dp[i - 1][j] + matrix[i][j],
                        (j == 0 ? numeric_limits<int>::max()
                                : dp[i - 1][j - 1] + matrix[i][j]),
                        (j == matrix[i].size() - 1
                             ? numeric_limits<int>::max()
                             : dp[i - 1][j + 1] + matrix[i][j])};
        dp[i][j] = *min_element(cmp.begin(), cmp.end());
      }
    }
    return *min_element(dp[matrix.size() - 1].begin(),
                        dp[matrix.size() - 1].end());
  }
};
```


