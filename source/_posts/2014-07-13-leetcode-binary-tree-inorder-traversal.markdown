---
layout: post
title: "LeetCode: Binary Tree Inorder Traversal"
date: 2014-07-13 20:55:23 +0800
comments: true
categories: Algorithm LeetCode
---
##  思路
同样是用显式栈

碰到的问题：不重复访问左子结点

## 代码
```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode *root) {
        vector<int> ans;
        if (root == NULL) return ans;
        TreeNode * stk[100];
        int top = 0;
        TreeNode *x = root;
        while (true) {
            if (x == NULL) {
                if(top > 0) {
                    x = stk[--top];
                    ans.push_back(x->val);
                    x = x->right;
                } else {
                    break;
                }
            } else { 
                //cout << x->val << endl;
                if (x->left != NULL) {
                    stk[top++] = x;
                    assert (top <= 100);
                    x = x->left;
                } else {
                    ans.push_back(x->val);
                    x = x->right;
                }
            }
        }
        return ans;
    }
};
```
