---
layout: '../../layouts/MarkdownPost.astro'
title: '安装flask'
pubDate: 2024-04-01
description: '如何将tailwindcss装到flask项目中'
author: '混沌爬行者'
cover:
    url: 'https://www.z4a.net/images/2023/03/19/-2023-03-19-201556.png'
    square: 'https://www.z4a.net/images/2023/03/19/-2023-03-19-201556.png'
    alt: 'cover'
tags: ["速查表", "学习开发笔记"]
theme: 'light'
featured: false
---
## 安装环境
npm，flask，pycharm
## 步骤
1. 按照[官网](https://tailwindcss.com/docs/installation/using-postcss)的步骤，在项目位置打开命令行终端运行命令
2. 运行完毕后在根目录创建`postcss.config.js`文件
3. 按照官网的内容，在对应的``tailwind.config.js``中创建对应的内容，修改对应的文件路径
```
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{html,js}"], #需修改
  theme: {
    extend: {},
  },
  plugins: [],
}
```
4. 在``static``中创建``input.css``和``output.css``文件，负责css的编译输出。在前者中复制进官网的对应内容。
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
5. 创建一个带有tailwindcss写法的html至``template``文件夹中，使用``render_template("index.html")``测试，将html中的``  <link href="/./static/src/input.css" rel="stylesheet">``的路径修改成自己项目对应文件的相对路径
6. ``npx tailwindcss -i ./src/input.css -o ./src/output.css --watch``修改这个命令中的文件位置为自己项目中文件的位置，运行该命令，正常显示则成功
7. （可选）在``package.json``中将该命令添加至启动命令中，使用``npm run [command]``启动
```
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="/./static/src/input.css" rel="stylesheet">
</head>
<body>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</body>
</html>
```