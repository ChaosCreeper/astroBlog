---
layout: '../../layouts/MarkdownPost.astro'
title: '从两个案例说起如何排查bug'
pubDate: 2023-06-30
description: '总是遇到别人遇不到的问题大多数是自己有问题'
author: '混沌爬行者'
cover:
    url: 'https://www.z4a.net/images/2023/07/12/nmd_wsm.jpg'
    square: 'https://www.z4a.net/images/2023/07/12/nmd_wsm.jpg'
    alt: 'cover'
tags: ["学习开发笔记","Bug汇总"]
theme: 'light'
featured: false
---

# BUG
## 1. 使用MybatisPlus进行CRUD时遇到的bug
### 现象
- 在当CRUD boy写简单接口时遇到了如下报错:
```
org.mybatis.spring.MyBatisSystemException:
nested exception is org.apache.ibatis.type.TypeException:
Could not set parameters for mapping: ParameterMapping{property='xxx', mode=IN, javaType=class java.xxx, jdbcType=VARCHAR, numericScale=null, resultMapId='null', jdbcTypeName='null', expression='null'}. 
Cause: org.apache.ibatis.type.TypeException: Error setting non null for parameter #3 with JdbcType VARCHAR . 
Try setting a different JdbcType for this parameter or a different configuration property. 
...
```

### 解决过程
1. 尝试网上的所有方案(无果)

- 在网上从CSDN和cnblog等中文论坛找到stackoverFlow,他们报错的结果大致如下:
    1. 在SQL语句中输入参数多写了单引号或者用了$而不是#
    2. Date类型要特别去指定但是没有指定,即JDBC类型出问题了
    - 以上的报错和相关的解决方法没有对我产生帮助,于是我开始自己解决

2. 使用控制变量法的措施寻找出问题的点(无果)

- 在寻找的过程中我发现自己另外一个部分的CRUD接口是没有出问题的,那么我可以去对照查看
    - 但是很遗憾,我一对一把所有写的代码对照了一遍,并且用相同的方式去重写了测试,还是不能找到问题
    - 同时,我也写了测试方法,确定了问题就是出在了mybatis上,但是找不到问题的所在

3. 于是我放弃了,然后随意的看错误堆栈(成功)

- 最后在万念俱灰之下我发现了自己的表名那出现了不该出现的一个单引号,罪魁祸首被找到了

### 总结

- 这是一次好的寻找bug的过程,充分体现了我眼瞎的特性,但是不失为一次排查的参考


## 2. 在使用JSCH的写操作模块时遇到的问题
### 现象
- 在尝试使用jsch编写一个可以整合FTP服务器上传下载操作文件和运行命令的模块时出现了问题,exec模式总是无法得到输出

### 解决过程
- 形如1,但是最后没有找到问题所在,所以我求助他人,在大佬的的仔细排查下他发现了问题,即在exec模式下connect方法一旦执行就不会再执行命令了,不能使用sftp模式下的流程,二者耦合不能

### 总结
- 这一个月的开发实习让我充分的认识到了自己在批判性思考这方面还是相当欠缺的,我不能在这些时候去做一个批判性的思考从而高效的排查bug
- 无论在哪批判性思维都很重要啊,可是我没有(悲)
