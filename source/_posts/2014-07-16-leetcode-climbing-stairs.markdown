---
layout: post
title: "LeetCode: Climbing Stairs"
date: 2014-07-16 18:42:36 +0800
comments: true
categories: 
---
## 思路
到第n层的方法数 ＝ 到第 n-1 层 + 到第 n-2 层

其实是个斐波那契数列

## 代码
```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n == 0) return 1;
        if (n == 1) return 1;
        int a = 1;
        int b = 1;
        int c = 0;
        for (int i = 1; i < n; ++i) {
            c = a + b;
            a = b;
            b = c;
        }
        return b;
    }
};
```