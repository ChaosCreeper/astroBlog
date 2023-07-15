---
layout: '../../layouts/MarkdownPost.astro'
title: '蓝桥杯在线练习系统的Bug?'
pubDate: 2023-03-15
description: 'print(input())'
author: '混沌爬行者'
cover:
    url: https://www.z4a.net/images/2023/03/15/printinput.png
    square: 'https://www.z4a.net/images/2023/03/15/printinput.png'
    alt: 'cover'
tags: ["开发学习笔记", "吐槽"]
theme: 'light'
featured: false
---

- 今日在蓝桥杯刷题,偶然发现了在python的编译环境下对一些填空题类型的算法题输入`print(input())`
可以直接的得到一个AC

- 如:
    - [杨辉三角](https://www.lanqiao.cn/problems/1457/learning/?page=2&first_category_id=1&sort=students_count&second_category_id=3&tags=省赛)
    - [第几天](https://www.lanqiao.cn/problems/614/learning/?page=4&first_category_id=1&sort=students_count&second_category_id=3&tags=省赛)
- 等题目是可以直接AC的
- 但是在类似于:
    - [承压计算](https://www.lanqiao.cn/problems/647/learning/?page=4&first_category_id=1&sort=students_count&second_category_id=3&tags=省赛)
    的题目上是行不通的

~~也许正式比赛可以用~~



