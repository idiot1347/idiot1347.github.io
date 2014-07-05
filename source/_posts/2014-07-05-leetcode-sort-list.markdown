---
layout: post
title: "LeetCode: Sort List"
date: 2014-07-05 23:45:49 +0800
comments: true
categories: Algorithm LeetCode
---


重学基本的算法，以前还是太不用心，太急躁了。

## 链表的快排
写了挺久，碰到的主要问题是：

1. 分别排序两个子链表时没有把子链表的最后一个结点的 next 设为 NULL；
2. 链接左子链表，head，右子链表时检查 u 是否为 NULL；
3. 最坏时间复杂度：在划分时如果结点的值和 head 的值相同就根据结点序号的奇偶性来决定放到左子链表还是右子链表中；

上代码
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *sortList(ListNode *head) {
        //printf("%d\n", head);
        //if (head != NULL)
            //printf("%d %d\n", head->next, head->val);
        if (head == NULL || head->next == NULL) return head;
        //printf("c\n");
        ListNode *p = new ListNode(-1);
        ListNode *q = new ListNode(-1);
        ListNode *u = p;
        ListNode *v = q;
        ListNode *w = head->next;
        int idx = 0;
        while (w != NULL) {
            //printf("%d\n", w->val);
            if (w->val < head->val)  {
                u->next = w;
                u = w;
            } else if (w->val > head->val) {
                v->next = w;
                v = w;
            } else {
                if (idx & 1) {
                    u->next = w;
                    u = w;
                } else {
                    v->next = w;
                    v = w;
                }
            }
            w = w->next;
            ++idx;
        }      
        u->next = NULL; //orz
        v->next = NULL; //orz
        u = sortList(p->next);
        v = sortList(q->next);
        if (u == NULL)
            u = head;
        w = u;
        //printf("u%d v%d w%d\n", u, v, w);
        //printf("%d %d %d\n", u->next, v->next, w->next);

        //printf("%d %d %d\n", w, w->next, w->next->next);
        while (w->next != NULL) {
            w = w->next;
            //printf("%d\n", w);
        }
        //printf("abc\n");
        if (u != head) //orz
            w->next = head;
        head->next = v;
        delete p;
        delete q;
        //printf("def\n");
        return u;
    }
};
```