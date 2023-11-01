---
layout: '../../layouts/MarkdownPost.astro'
title: '如何在Vue2的项目中使用tailwindCSS'
pubDate: 2023-11-1
description: '网上的参考都不行,所以自己写一个'
author: '混沌爬行者'
cover:
    url: 'https://www.z4a.net/images/2023/03/19/-2023-03-19-201556.png'
    square: 'https://www.z4a.net/images/2023/03/19/-2023-03-19-201556.png'
    alt: 'cover'
tags: ["痛苦环境搭建之路", "学习开发笔记"]
theme: 'light'
featured: false
---

## 背景
- 本来想学习scss的,但是看完[这个东西](https://stateofcss.com/)之后,想试试tailwindCSS
- 网上的参考那叫一个乱,最后我决定自己按照使用Vue的经验和脑子去依照官网的指导依葫芦画瓢安装

## 如何安装
- 原生HTML用户去看[官方文档](https://www.tailwindcss.cn/)
- *初次实践*: 对Vue2开发者来说,目前网上的安装资料说法不一致,需要自己去尝试安装
	- 官方文档的`npx tailwindcss -i ./src/input.css -o ./dist/output.css --watch`命令使用时不知为何会无法停止,所以对我来说目前安装官方文档步骤,获取`output.css`然后导入全局是无法使用的
	- 另一方面,仅仅是做到`将加载 Tailwind 的指令添加到你的 CSS 文件中`这一步后直接将css文件导入`main.js`是没有用的
	- 但是经过我的尝试,我发现`npx tailwindcss -i ./src/input.css -o ./dist/output.css --watch`要自己关掉,然后将编译的结果css导入至main.js即可使用
		- 但是每次修改都会需要把服务器关掉再次编译,这就令人难以接受
- VSCode有个相关的[代码预览插件](https://cn.windicss.org/editors/vscode.html)需要装,方便开发
- *升级改进*: 使用更多的插件/依赖实现即时编译
	- 点击官方网站上的[这个页面](https://www.tailwindcss.cn/docs/installation/using-postcss)你就可以发现官方针对这个问题对大部分前端框架项目做了解决
		- 无需指定下载某个特定版本,按照官网的步骤走是没有问题的
	- 所以,你需要按照官网的步骤走,但是稍作修改
		- 在`npx tailwindcss init`后你需要自己创建`postcss.config.js`然后安装官网指导将对应内容写入
		- `Configure your template paths`在这一步你需要在后缀识别中加入`vue`,并且将public的index.html也加入
		- `Add the Tailwind directives to your CSS`在这一步你需要将创建好的css文件直接导入`main.js`
		- `npm run serve`后你将可以看见它可以正常使用了 
- 可以成功使用的标志是logo移位了/你自己加的tailwindcss代码正常显示
- 最后最好在VScode中添加一个插件`Tailwind CSS IntelliSense`,方便预览和参考