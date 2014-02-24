---
layout: post
status: publish
published: true
title: Language Grid调研结果[i]
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "<style>\r\n\t#eng {\r\n\t\tcolor:#999999;\r\n\t}\r\n\t#content {\r\n\t\tcolor:#555555;\r\n\t}\r\n\t#note
  {\r\n\t\tcolor:#222222;\r\n\t}\r\n</style>\r\n<div id=\"top\">\r\n        Language
  Grid工具箱<span id=\"eng\">Language Grid Toolbox</span>提供四项主要的服务是:\r\n\t<ul>\r\n\t\t* 翻译\r\n\t\t* 创建语言资源\r\n\t\t* 社区\r\n\t\t* 多语言论坛\r\n\t</ul>\r\n"
wordpress_id: 105
wordpress_url: http://blog.oneplus.info/?p=105
date: 2011-02-25 19:42:01.000000000 +08:00
categories:
- 可以控制
- HIT CIR
- Language Grid调研
tags:
- CIR
- Language Grid
comments: []
---
<style>
  #eng {
    color:#999999;
  }
  #content {
    color:#555555;
  }
  #note {
    color:#222222;
  }
</style>

Language Grid工具箱<span id="eng">Language Grid Toolbox</span>提供四项主要的服务是:

* 翻译
* 创建语言资源
* 社区
* 多语言论坛

### 翻译<span id="eng">(Translation)</span>

Toolbox提供的翻译功能是机器翻译结果。翻译功能由两个子功能组成，分别是

* 文本翻译
* 网页翻译

这两项功能和我们常见的Google Translation，或者翻译软件是相似的。不同之处是，文本翻译除了提供翻译功能之外，还提供回译<span id="eng">(back translation)</span>功能。按照帮助文档上提供的信息，回译的主要用于检查翻译的结果是否正确。

### 创建语言资源<span id="eng">(Language Resource Creation)</span>

Toolbox提供的创建语言资源的功能。介绍文档上说明这一功能的用途是，“Toolbox的用户可以创建自己的多语言词典，并且和机器翻译结合，以提高机器翻译结果的质量”<span id="eng">(community members can create their multilingual dictionaries, and combine them with machine translators to improve the translation quality.)</span>

创建语言资源主要包括以下子功能

* 词典<span id="eng">(dictionary)</span>
* 平行文本<span id="eng">(parallel text)</span>
* 网页<span id="eng">(web)</span>
* 术语<span id="eng">(glossary)</span>

#### DICTIONARY - 词典资源创建

词典的功能和通常意义上的词典是一样的。词典相当于一张表，其结构如下：

<table class="table" width="100%">
  <tr><td></td><td>Language<sub>1</sub></td><td>Language<sub>2</sub></td><td>...(可以添加)</td></tr>
  <tr><td>Record<sub>1</sub></td><td>...</td><td>...</td><td>...</td></tr>
  <tr><td>Record<sub>2</sub></td><td>...</td><td>...</td><td>...</td></tr>
  <tr><td>...(可以添加)</td></td><td>...</td><td>...</td><td>...</td></tr>
</table>

用户可以创建一个词典，向其中添加/编辑/删除 语言或记录。同时，词典可以设置修改级别。

#### PARALLEL_TEXT - 平行文本资源创建

可以进行整句翻译或者是整段翻译，其组织形式与Dictionary类似。

#### WEB - 网页资源创建

从试用的过程来看，网页这一功能大概的工作过程如下：

1. 将用户输入的网址的内容趴下来
2. 将标签间的内容一条一条呈现出来
3. 提供机器翻译结果
4. 用户可以修改机器翻译的结果

其具体使用方法和dictionary还有parallel_text是很像的。

#### GLOSSARY - 术语翻译创建

除了像dictionary那样有多语言翻译。glossary功能中，每个record还有属性列。每个record的属性可能是term,categories,define。而term属于categories，并且被一条或多条define定义。

#### TEMPLATE - 模板翻译创建

模板翻译是针对下面例子中的翻译需求，

<table class="table" width="100%">
  <tr><td></td><td>zh</td><td>en</td></tr>
  <tr><td>例句一</td><td>很多<u>树懒</u>栖息在同伴周围</td><td>Many <u>sloth</u> inhabit in his neighborhood</td></tr>
  <tr><td>例句二</td><td>很多<u>黑猩猩</u>栖息在同伴周围</td><td>Many <u>gorilla</u> inhabit in his neighborhood</td></tr>
</table>

例句一二的翻译，只需要调换一下两种动物。

在TEMPLATE中，每个record的属性可能是parallel_text,categories,parament,word。word属于pararment，对应例句中的sloth和gorilla，parament包含于parallel_text，是模板中可替换的内容的符号化表示。parallel_text对应翻译模板，属于categories。

##### 模板翻译

<table class="table" width="100%">
  <tr><td>zh</td><td>en</td></tr>
  <tr><td>很多<u>[1]</u>栖息在同伴周围</td><td>Many <u>[1]</u> inhabit in his neighborhood</td></tr>
</table>

##### 词汇翻译

<table class="table" width="100%">
  <tr><td>参数</td><td>zh</td><td>en</td></tr>
  <tr><td>[1]</td><td>树懒</td><td>sloth</td></tr>
  <tr><td>[1]</td><td>黑猩猩</td><td>gorilla</td></tr>
</table>

#### 社区<span id="eng">(Community)</span>

社区这一功能提供的各项服务可以很好地用其各自的名称来描述，其大致的目标是构建一个用户之间的协作平台。

* 文件共享<span id="eng">File sharing</span>
* 任务管理<span id="eng">Task Management</span>
* 共同翻译<span id="eng">Collaborative Translation</span>

完整结果请点击<a href="http://blog.oneplus.info/nlp/langrid.html">这里</a>
