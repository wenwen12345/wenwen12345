---
title: "Leetcode每日一题2023 7 12"
date: 2023-07-12T18:41:03+08:00
tag: 
    - cpp
    - leetcode
    - 编程
draft: true
---

# leetcode 每日一题

今天的[每日一题][today]是一道简单题，可以使用一点简单的技巧。

## 思路

建立一个字符串来遍历题目给出的数字,
建立一个 flag 变量, 储存当前的符号位,
使用 for 循环, 遍历字符串中的每一位数字, 加上符号，加到结果里。

使用字符串是应为可以直接 `std::to_string()` 方便, 可以使用 range based for 遍历。

## 代码

```cpp
#include <string>
class Solution {
public:
    int alternateDigitSum(int n) {
        auto n_string = std::to_string(n);
        bool flag = true;
        int res = 0;
        for (auto&&i:n_string) {
            res += (!(flag = !flag)?1:-1) * (i - '0');
        }
        return res;
    }
};
```

其中 `(!(flag = !flag)?1:-1)` 可以使用 `(2 * !(flag = !flag) - 1)` 代替，`!(flag = !flag)` 是用来使用 flag 后反转 flag。 `i - '0'` 用来将 i转换成数字。

[today]: https://leetcode.cn/problems/alternating-digit-sum/description/
