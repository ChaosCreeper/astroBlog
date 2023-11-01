---
layout: '../../layouts/MarkdownPost.astro'
title: '吐槽写反转链表题解的人'
pubDate: 2023-04-23
description: '我去你妈的双指针'
author: '混沌爬行者'
cover:
    url: ''
    square: ''
    alt: 'cover'
tags: ["学习开发笔记", "算法学习"]
theme: 'light'
featured: false
---
[反转链表](https://leetcode.cn/problems/reverse-linked-list/)

### 抱怨
- 为什么,为什么要叫双指针,你们他妈的脑袋被驴踢了是不是,我想了一个小时,怎么也想不通要怎么只用两个指针解决题目
- fine, let me see the solution

```
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* cur = NULL, *pre = head;
        while (pre != NULL) {
            ListNode* t = pre->next;
            pre->next = cur;
            cur = pre;
            pre = t;
        }
        return cur;
    }
};
```

```
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (head == NULL) { return NULL; }
        ListNode* cur = head;
        while (head->next != NULL) {
            ListNode* t = head->next->next;
            head->next->next = cur;
            cur = head->next;
            head->next = t;
        }
        return cur;
    }
};
```

- 告诉我,这里面用了几个指针,三个,三个啊,你们是瞎了吗,`ListNode* t = pre->next;`,看不见这个指针是不是,我本来以为动态规划这种直接翻译已经够傻了,这还有个更离谱的.

- 气死我了,气死我了

### 悲伤
- 我好没用,我怎么连这种程度的哄骗都识破不了
- 我好没用,要画草稿才能想到具体的解法,他们就在脑子里想就能解题了

