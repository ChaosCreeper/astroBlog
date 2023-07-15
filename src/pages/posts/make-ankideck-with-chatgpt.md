---
layout: '../../layouts/MarkdownPost.astro'
title: '使用chatgpt生成简单的Oxford5000的anki卡片'
pubDate: 2023-04-17
description: '核电煮水式批量生成anki单词卡'
author: '混沌爬行者'
cover:
    url: 'https://www.z4a.net/images/2023/04/16/-2023-04-16-23493743d6c92f7e0ed28b.png'
    square: 'https://www.z4a.net/images/2023/04/16/-2023-04-16-23493743d6c92f7e0ed28b.png'
    alt: 'cover'
tags: ["学习开发笔记", "赛博萨满の经验", "英语学习"]
theme: 'light'
featured: false
---

### 事情的起因
- 因为一个个把[oxford5000](https://www.oxfordlearnersdictionaries.com/wordlists/oxford3000-5000)的单词一个个按照[longman](https://www.ldoceonline.com/dictionary/)词典录入太累了,所以我打算偷懒

### 理想的计划的失败
- 研究研究那网站的结构,然后用python的爬虫爬个爽,直接存进文本文件里,然后存进anki里
- 哎呀,好像可以直接让chatgpt生成出来:

```
import requests
from bs4 import BeautifulSoup

url = 'https://www.oxfordlearnersdictionaries.com/wordlists/oxford3000-5000'
response = requests.get(url, verify=False)

soup = BeautifulSoup(response.content, 'html.parser')

words = []

for row in soup.find_all('tr')[1:]:
    columns = row.find_all('td')
    word = columns[1].text.strip()
    if word not in words:
        words.append(word)

with open('oxford5000_excluding_oxford3000.txt', 'w') as file:
    for word in words:
        file.write(word + '\n')

result = "The words from the Oxford 5000 excluding Oxford 3000 list have been extracted and saved as a text file."

print(result)
```

- 然而事情没有那么简单就成了,在使用pycharm运行之后这段程序就会卡住,拿到jupyter运行就会这样

```
ProxyError: HTTPSConnectionPool(host='www.oxfordlearnersdictionaries.com', port=443): Max retries exceeded with url: /wordlists/oxford3000-5000 (Caused by ProxyError('Cannot connect to proxy.', FileNotFoundError(2, 'No such file or directory')))
```

```
SSLError: HTTPSConnectionPool(host='www.oxfordlearnersdictionaries.com', port=443): Max retries exceeded with url: /wordlists/oxford3000-5000 (Caused by SSLError(SSLEOFError(8, 'EOF occurred in violation of protocol (_ssl.c:1131)')))
```

- 好,毫不意外的失败了!到处查了查,这让人烦心,不整了

### 萨满の灵光一闪
- 怎么办呢,最后就把这玩意丢到记忆的角落里不管了,但是我最近又听到有人在吹auto-gpt和agent-gpt,好奇试了试,为什么它们可以访问网站爬取数据我不能,见了鬼了,但是单纯的试了试我发觉在这个问题上它好像没啥用,我还不如直接用chat-gpt自己一个个刷出来呢
- 我猜它虽然不能访问字典网站,但是应该有那个资料,应该可以用一些类似把它变成猫娘的咒语弄出来
- 于是就有了封面![萨满咒语](https://www.z4a.net/images/2023/04/16/-2023-04-16-23493743d6c92f7e0ed28b.png "萨满咒语")

### 如何在得到结果之后导入
- 力大砖飞,当然是一个个复制黏贴到txt文本里,然后把它转成csv文件,然后在anki里做好对应的模板,确定好分隔符导入,总之,结果还是令人满意的:

~~我是不会告诉你以为要先导入excel再导入anki所以和如何修改分隔符大战了一个晚上的~~

```
establish::The company plans to establish a new office in Tokyo; to set up or create something, typically a business or organization.
estate::The family's estate was divided among their heirs; all the money and property owned by a person, especially at death.
estimate::The contractor provided an estimate for the cost of the project; to roughly calculate or judge the value, number, quantity, or extent of something.
```
