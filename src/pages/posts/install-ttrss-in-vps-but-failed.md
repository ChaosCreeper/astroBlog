---
layout: '../../layouts/MarkdownPost.astro'
title: '尝试在云服务器上搭建ttrss但是知难而退了!所以FreshRSS真方便!'
pubDate: 2023-03-19
description: '尝试在没有域名的腾讯云服务器上搭建rss服务但是因为麻烦事情太多所以先不干了!最后了解了一大堆东西之后还是FressRSS好装!'
author: '混沌爬行者'
cover:
    url: 'https://www.z4a.net/images/2023/03/19/-2023-03-19-201556.png'
    square: 'https://www.z4a.net/images/2023/03/19/-2023-03-19-201556.png'
    alt: 'cover'
tags: ["痛苦环境搭建之路", "学习开发笔记"]
theme: 'light'
featured: false
---
## 麻烦的开始
- 尝试在腾讯云主机上搭建一个rss,本来想着一下子就可以弄好,但是使用这个[教程](https://sspai.com/post/41302)搭的服务不知道为什么总是冒出"60 SSL certificate problem certificate has expired"之类的问题无法正常的订阅rss
    - 寻找了一番之后发现好像是ssl证书的问题,但是对现在的我来说那些东西看的一头雾水,所以我决定再找一个教程重新部署一遍
## 于是乎..
- 然后我找到了一个看起来比较好的[awesome-ttrss官方文档](https://ttrss.henry.wang/zh/#%E5%85%B3%E4%BA%8E),但是我发现这个又需要一些更加麻烦的东西:
    1. 我没有下载的docker compose
    2. 需要docker compose下载部署的awesome-ttrss
    3. 安装配置我没学过的postgresSQL,以及我没有学过的不知道如何处理的docker-compose.yml 
    4. 安装配置ngnix
- 难啊!整的我难受啊,我又想要在地面阴暗的爬行了,所以我绝望的尝试用搜索引擎查找那些可以用的教程,直接搜少之又少,所以我另辟蹊径用类似"ngnix配置/安装+rss"的关键词搜到了一些看起来有用的
## 归档
- 但是这番折腾已经过去了一个下午到了晚上了,我没有时间了,所以怀着失败和不甘的心情写下了这篇以后会修改成教程的文章,留作资源索引以后来看
    - 可能用得上的教程:
        1. [Docker搭建TTRSS——免费开源多平台RSS阅读器](https://blog.suysker.xyz/archives/138)
        2. [部署 Tiny Tiny RSS 遇见的坑](https://blog.kukmoon.com/fef91966/)
        3. [awesome-ttrss官方文档](https://ttrss.henry.wang/zh/#%E5%85%B3%E4%BA%8E)
        4. [Tiny Tiny RSS最新安装与使用教程-Awesome TTRSS Docker安装配置方法](https://wzfou.com/ttrss-docker/)
## 总结
~~我怎么感觉自己第一次只要整懂了那个60错误是怎么回事就完事了呢~~也许是因为我没有整域名或者什么ssl证书?,不过除了这个之外我也没有搞懂docker该怎么操作,以及怎么用ngnix,十分的失败

## 最后的最后
- 好了,我放弃整那一大堆的东西了,让那些东西见鬼去吧,FreshRSS真是方便好用,按照这个[链接](https://veryjack.com/technique/docker-install-freshrss/)去安装FreshRSS就可以了,你甚至不用去安装链接内的面板,直接装好启动初始化就行了!
