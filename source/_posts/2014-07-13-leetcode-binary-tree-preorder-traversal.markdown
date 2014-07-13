---
layout: post
title: "LeetCode: Binary Tree Preorder Traversal"
date: 2014-07-13 19:41:58 +0800
comments: true
categories: Algorithm LeetCode
---

## 思路
只是把隐式栈改成了显式栈罢了

## 代码
```cpp
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> preorderTraversal(TreeNode *root) {
        vector<int> ans;
        if (root == NULL) return ans;
        stack<TreeNode *> stk;
        TreeNode *x = root;
        while (true) {
            ans.push_back(x->val);
            if (x->left != NULL) {
                if (x->right != NULL) {
                    stk.push(x->right);
                }
                x = x->left; // 先入栈，后修改x
            } else if (x->right != NULL) {
                x = x->right;
            } else if (!stk.empty()) {
                x = stk.top();
                stk.pop();
            } else {
                break;
            }
        }
        return ans;
    }
};
```