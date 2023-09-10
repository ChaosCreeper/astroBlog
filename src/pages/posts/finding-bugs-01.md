---
layout: '../../layouts/MarkdownPost.astro'
title: '痛苦的前端开发环境安装'
pubDate: 2023-06-30
description: '为什么我总是会遇到这些别人遇不到的问题(悲)'
author: '混沌爬行者'
cover:
    url: 'https://www.z4a.net/images/2023/07/12/nmd_wsm.jpg'
    square: 'https://www.z4a.net/images/2023/07/12/nmd_wsm.jpg'
    alt: 'cover'
tags: ["学习开发笔记","Bug汇总"]
theme: 'light'
featured: false
---

# 安装node环境遇到的从来没见过的bug
## 现象
1. node和npm等能在system32目录下和powershell等地方正常操作,在用户目录下输入操作结果为空
2. 使用vue或npm run serve等命令出现大致如下内容:
```ERROR: b#4e(乱码)不是命令或.....```
2. node_modules被安装在了system32的文件夹内
3. npm local pperfix 和 cwd 路径全是system32, home是C的用户文件夹

## 解决办法
1. 真是见鬼了,原来是公司加密软件的问题,我说怎么从来没见过这个错误,网上也找不到
2. 路径问题把路径改了就行,其实NODE_PATH似乎是不用去配的,安装完成了就行