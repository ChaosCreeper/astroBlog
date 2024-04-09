---
layout: '../../layouts/MarkdownPost.astro'
title: 'lxml快查表'
pubDate: 2023-03-19
description: '学习完lxml后的速查表'
author: '混沌爬行者'
cover:
    url: 'https://www.z4a.net/images/2023/03/19/-2023-03-19-201556.png'
    square: 'https://www.z4a.net/images/2023/03/19/-2023-03-19-201556.png'
    alt: 'cover'
tags: ["速查表", "学习开发笔记"]
theme: 'light'
featured: false
---
## 标签树结构相关的操作
### 创建树结构
- 创建根节点
``>>> root = etree.Element("root")``
- 添加子节点
``root.append( etree.Element("child1") )``或
``child2 = etree.SubElement(root, "child1")``
### 输出树结构
- 输出单个节点
``print(root.tag)``
- 格式化输出树结构
``prettyprint(root)``
### 以列表的方式操作树结构
- 使用下标访问单个
``print(root[0].tag)``
- 获取节点数量
``print(len(root))``
- 获取当前访问节点下标
``root.index(root[1])``
- 使用列表和循环操作
  ```
  children = list(root)
  for child in root:
        print(child.tag)
  ```
- 插入节点
``root.insert(0, etree.Element("child0"))``
- 访问首节点尾节点
  ```
  print(root[:1][0].tag)
  print(root[-1:][0].tag)
  ```
### 其他
- 检查是否是父节点
``root is root[0].getparent()  # lxml.etree only!``
- 访问前节点
``root[0] is root[1].getprevious() # lxml.etree only!``
- 访问后节点
``root[1] is root[0].getnext() # lxml.etree only!``
- 复制树结构
```
element = etree.Element("neu")
element.append( deepcopy(root[1]) )
```
- 移除操作
```
root[0] = root[-1]  # this moves the element in lxml.etree!
for child in root:
     print(child.tag)
```
### 属性访问
#### 基础方法
- 创建方法1
``root = etree.Element("root", interesting="totally")``
- 创建方法2
``root.set("hello", "Huhu")``
- 访问对应键值方法
``print(root.get("interesting"))``
- 获取所有的键
``sorted(root.keys())``
#### 其他方法
- 访问方法
``attributes = root.attrib``
``print(attributes["interesting"])``
``print(attributes.get("no-such-attribute"))``
- 创建方法
``attributes["hello"] = "Guten Tag"``
``print(attributes["hello"])``
``print(root.get("hello"))``
- 使用``dict``获取全部
```
>>> d = dict(root.attrib)
>>> sorted(d.items())
[('hello', 'Guten Tag'), ('interesting', 'totally')]
```
### 标签内文字
- 赋值方法
``root.text = "TEXT"``
- 示例，构建DOM
```
>>> html = etree.Element("html")
>>> body = etree.SubElement(html, "body")
>>> body.text = "TEXT"

>>> etree.tostring(html)
b'<html><body>TEXT</body></html>'

>>> br = etree.SubElement(body, "br")
>>> etree.tostring(html)
b'<html><body>TEXT<br/></body></html>'

>>> br.tail = "TAIL"
>>> etree.tostring(html)
b'<html><body>TEXT<br/>TAIL</body></html>'
```
- 格式化输出
```
>>> etree.tostring(br)
b'<br/>TAIL'
>>> etree.tostring(br, with_tail=False) # lxml.etree only!
b'<br/>'
```
## 查找标签内容
- 使用xpath寻找所有的text,返回列表
``print(html.xpath("//text()")) # lxml.etree only!``
- 获取第一个找到的text
``print(html.xpath("string()"))``
- 作为函数，使用示例
```
>>> build_text_list = etree.XPath("//text()") # lxml.etree only!
>>> print(build_text_list(html))
['TEXT', 'TAIL']
```
- 通过查找的对象获取其父标签/同级标签
```
>>> texts = build_text_list(html)
>>> print(texts[0])
TEXT
>>> parent = texts[0].getparent()
>>> print(parent.tag)
body

>>> print(texts[1])
TAIL
>>> print(texts[1].getparent().tag)
br
```
- 内容类型判断
```
>>> print(texts[0].is_text)
True
>>> print(texts[1].is_text)
False
>>> print(texts[1].is_tail)
True
```
### 遍历对象
- 获取遍历对象
``for element in root.iter(): print(f"{element.tag} - {element.text}")``
- 过滤获取标签
``for element in root.iter("child"): print(f"{element.tag} - {element.text}")``
- 过滤获取多个标签
``for element in root.iter("another", "child"):...``
- 处理特殊标签属性
```
>>> root.append(etree.Entity("#234"))
>>> root.append(etree.Comment("some comment"))

>>> for element in root.iter():
...     if isinstance(element.tag, str):
...         print(f"{element.tag} - {element.text}")
...     else:
...         print(f"SPECIAL: {element} - {element.text}")
root - None
child - Child 1
child - Child 2
another - Child 3
SPECIAL: &#234; - &#234;
SPECIAL: <!--some comment--> - some comment

>>> for element in root.iter(tag=etree.Element):
...     print(f"{element.tag} - {element.text}")
root - None
child - Child 1
child - Child 2
another - Child 3

>>> for element in root.iter(tag=etree.Entity):
...     print(element.text)
&#234;
```
### 序列化
- 设置xml声明，编码及其他
```
>>> root = etree.XML('<root><a><b/></a></root>')

>>> etree.tostring(root)
b'<root><a><b/></a></root>'

>>> xml_string = etree.tostring(root, xml_declaration=True)
>>> print(xml_string.decode(), end='')
<?xml version='1.0' encoding='ASCII'?>
<root><a><b/></a></root>

>>> latin1_bytesstring = etree.tostring(root, encoding='iso8859-1')
>>> print(latin1_bytesstring.decode('iso8859-1'), end='')
<?xml version='1.0' encoding='iso8859-1'?>
<root><a><b/></a></root>

>>> print(etree.tostring(root, pretty_print=True).decode(), end='')
<root>
  <a>
    <b/>
  </a>
</root>
```
- 特殊字符的处理
```
>>> root = etree.XML('<root><a><b/>\n</a></root>')
>>> print(etree.tostring(root).decode())
<root><a><b/>
</a></root>

>>> etree.indent(root)
>>> print(etree.tostring(root).decode())
<root>
  <a>
    <b/>
  </a>
</root>

>>> root.text
'\n  '
>>> root[0].text
'\n    '

>>> etree.indent(root, space="    ")
>>> print(etree.tostring(root).decode())
<root>
    <a>
        <b/>
    </a>
</root>

>>> etree.indent(root, space="\t")
>>> etree.tostring(root)
b'<root>\n\t<a>\n\t\t<b/>\n\t</a>\n</root>'
```
- 直接导出文字
```
>>> root = etree.XML(
...    '<html><head/><body><p>Hello<br/>World</p></body></html>')
>>> etree.tostring(root, method='text')
b'HelloWorld'
```
- 设定编码文字
```
>>> br = next(root.iter('br'))  # get first result of iteration
>>> br.tail = 'Wörld'

>>> etree.tostring(root, method='text')  # doctest: +ELLIPSIS
Traceback (most recent call last):
  ...
UnicodeEncodeError: 'ascii' codec can't encode character '\xf6' ...

>>> etree.tostring(root, method='text', encoding="UTF-8")
b'HelloW\xc3\xb6rld'
```
## ElementTree
- 设置根节点的特殊属性
```
>>> root = etree.XML('''\
... <?xml version="1.0"?>
... <!DOCTYPE root SYSTEM "test" [ <!ENTITY tasty "parsnips"> ]>
... <root>
...   <a>&tasty;</a>
... </root>
... ''')

>>> tree = etree.ElementTree(root)
>>> print(tree.docinfo.xml_version)
1.0
>>> print(tree.docinfo.doctype)
<!DOCTYPE root SYSTEM "test">

>>> tree.docinfo.public_id = '-//W3C//DTD XHTML 1.0 Transitional//EN'
>>> tree.docinfo.system_url = 'file://local.dtd'
>>> print(tree.docinfo.doctype)
<!DOCTYPE root PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "file://local.dtd">
```


## 从其他的来源中构建标签树
### 简单构建
- 从字符串构建简单标签树
``root = etree.fromstring(some_xml_data)``
- 字符串构建xml
``etree.XML("<root>data</root>")``
- 字符串构建HTML，自动填充外部标签
``etree.HTML("<p>data</p>")``
- 二进制IO流读取构建
``tree = etree.parse(some_file_or_file_like_object)``
### ``Parser``自定义构建
- 去除b围绕之外的空格
```
parser = etree.XMLParser(remove_blank_text=True) 
root = etree.XML("<root>  <a/>   <b>  </b>     </root>", parser)
```
- 渐进式处理
- 事件驱动处理

## 命名空间

## E-factory

## ElementPath
- ``iterfind()`` 查找任何一处符合的，返回结果列表
- ``findall()`` 返回找到的结果列表，可添加特定的条件
```
>>> print(root.findall(".//a[@x]")[0].tag)
a
>>> print(root.findall(".//a[@y]"))
[]
```
- ``find()`` 效率返回找到的第一个
```
>>> print(root.find("b"))
None
>>> print(root.find("a").tag)
a
```
- ``findtext()`` 返回找到的第一个的文字内容

- 生成对应的path
```
root = etree.XML("<root><a x='123'>aText<b/><c/><b/></a></root>")
>>> tree = etree.ElementTree(root)
>>> a = root[0]
>>> print(tree.getelementpath(a[0]))
a/b[1]
>>> print(tree.getelementpath(a[1]))
a/c
>>> print(tree.getelementpath(a[2]))
a/b[2]
>>> tree.find(tree.getelementpath(a[2])) == a[2]
True
```

- 等价的搜索方法
```
>>> print(root.find(".//b").tag)
b
>>> print(next(root.iterfind(".//b")).tag)
b
>>> print(next(root.iter("b")).tag)
b
```

- 针对符合条件的节点搜索其附近同级的节点或者子级节点
```
heads = tree.findall(".//li[@class='font-size-3 color-yellow main-list-li']")
  for item in heads:
    sub_class = item.text.strip()
    class_link.append({'leave': sub_class, 'prev': category})
    body = item.getnext()
    # cn
    foods = body.findall(".//a[@class='text-light after-content']")
    for food in foods:
    res = food_collect.find_one({'common': food.text.strip()})
    if res:
      food_id = res['_id']
      link_collect.update_one({'food_id': food_id}, {'$set': {"category": sub_class}})
      # print(food_id)
    else:        
      print(food.text.strip())
print(sub_dict)
```