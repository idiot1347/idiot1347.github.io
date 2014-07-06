---
layout: post
title: "LeetCode: Search Insert Position"
date: 2014-07-06 00:12:00 +0800
comments: true
categories: Algorithm LeetCode
---

##　二分
碰到的问题： 没有考虑到数组中所有数字都比 target 小

##　代码
```cpp
class Solution {
public:
    int searchInsert(int A[], int n, int target) {
        int low = 0, high = n - 1;
        while (low < high) {
            int mid = (low + high) / 2;
            if (A[mid] < target)
                low = mid + 1;
            else
                high = mid;
        }
        if (A[low] >= target)
            return low;
        return low + 1;
    }
};
```