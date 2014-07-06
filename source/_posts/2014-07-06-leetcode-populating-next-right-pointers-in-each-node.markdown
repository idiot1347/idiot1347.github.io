---
layout: post
title: "LeetCode: Populating Next Right Pointers in Each Node"
date: 2014-07-06 11:57:26 +0800
comments: true
categories: Algorithm LeetCode
---

## 思路
就是一层一层的遍历，同时维护一个指针标记当前访问的左边的结点，本想用 bfs 但要用队列，不满足常数空间复杂度的要求；这里隐式用到了栈，是不是也不满足要求？（待解决）

碰到的问题：到达 max_depth 时忘了 return

## 代码
```cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        int height = 0;
        TreeLinkNode *p = root;
        while (p != NULL) {
            ++height;
            p = p->left;
        }
        for (int i = 1;i <= height;++i) {
            TreeLinkNode **p = new (TreeLinkNode *);
            *p = NULL;
            dfs(root, 0, i, p);
        }
    }
    
    void dfs(TreeLinkNode *current, int depth, int max_depth, TreeLinkNode **ptr) {
        if (depth == max_depth) {
            if (*ptr != NULL) {
                (*ptr)->next = current;
            }
            *ptr = current;
            return;
        }
        dfs(current->left, depth + 1, max_depth, ptr);
        dfs(current->right, depth + 1, max_depth, ptr);
    }
};
```
