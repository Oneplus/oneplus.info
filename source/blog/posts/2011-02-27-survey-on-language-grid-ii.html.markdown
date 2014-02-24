---
layout: post
status: publish
published: true
title: Language Grid调研结果[ii]
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "\t<div id=\"playground\">\r\n\t\t<strong>Language Grid Playground</strong>\r\n\t\tLanguage
  Grid面向组织机构的服务主要是由Playground完成。用户要注册Playground，需要向申请一个Group ID。\r\n\t\tPlayground提供给普通用户使用Language
  Grid中资源的接口，注册的组织机构也可以通过Language Grid获得相关的研究成果。\r\n\t\t由于没能申请到Group ID，我的调研只从普通用户的角度进行。\r\n\r\n"
wordpress_id: 112
wordpress_url: http://blog.oneplus.info/?p=112
date: 2011-02-27 15:07:48.000000000 +08:00
categories:
- 可以控制
- HIT CIR
- Language Grid调研
tags:
- CIR
- Language Grid
comments: []
---

### Language Grid Playground

Language Grid面向组织机构的服务主要是由Playground完成。用户要注册Playground，需要向申请一个Group ID。

Playground提供给普通用户使用Language Grid中资源的接口，注册的组织机构也可以通过Language Grid获得相关的研究成果。

由于没能申请到Group ID，我的调研只从普通用户的角度进行。

Playground提供的服务有三种级别，分别是：

#### Basic

* DICTIONARY - 多语言词典
* CONCEPT DICTIONARY - 概念词典
* PICTOGRAM - 图像词典
* PARALLEL TEXT - 文本词典
* MORPHOLOGICAL ANALYSIS - 语义分析
* DEPENDENCY PARASE - 语意依存分析

#### Advanced

* dictionary creation
* parallel creation
* categorized word creation
* composite translation
* document translation

#### CUSTOMIZE

其中，BASIC基本是用于普通用户从Language Grid中获得语言服务。ADVANCED则提供给注册用户创建词典等，CUSTOMIZED则是定制性的服务。

#### Basic

##### dictionary

词典功能单纯提供一个查词功能。

用户可以选择词语源语言和目标语言，还可以选择词语在词典中的匹配方式，并可以选择词典。playground会列出所有选择的词典中符合匹配方式的解释。

帮助文档中解释说这种查词方式的优势是：

1. 多部词典一起查，节约时间
2. 可以比较词典之间的查询结果

##### concepte dictionary

概念词典是用于解释词义的词典，使用方法与dictionary相同，可以选择源语言，词典。playground会列出所有的选择的词典中的概念，同义词和相关概念

举例说明：

查android，在WordNet中的解释是“an automaton that resembles a human being”
同义词是“android, humanoid, mechanical man (noun)”

~~~
=> automaton, robot, golem (a mechanism that can move automatically)
  => mechanism (device consisting of a piece of machinery, has moving parts that perform some function)
    => device (an instrumentality invented for a particular purpose)
      => instrumentality, instrumentation (an artifact (or system of artifacts) that is instrumental in accomplishing some end)
        => artifact, artefact (a man-made object taken as a whole)
          => whole, unit (an assemblage of parts that is regarded as a single entity)
            => object, physical object (a tangible and visible entity, an entity that can cast a shadow)
              => physical entity (an entity that has physical existence)
                => entity (that which is perceived or known or inferred to have its own distinct existence (living or nonliving))
~~~

由于概念的一般形式是“名词<sub>1</sub>”的概念是“名词<sub>2</sub>+定语”，相关概念的组织方法是用名词<sub>i</sub>解释名词<sub>i+1</sub>，直到名词<sub>t</sub>不能被解释为止。

##### pictogram

图像查询是建立单词和图像的一种联系。比方说输入smile，可能获得多种图片。

pictogram主要做的就是对于一种语言的输入，将其对应的图片输出。

帮助文档中解释说：

1. 只根据图像本身的属性获得从文字到图像的翻译是比较困难的，尤其是在多种语言的情况下
2. 从多种语言翻译到图像的一个比较好的解决方案是用大量的语言和数据去描述一幅图片，但这样做开销巨大
3. 解决这一问题的一个简单的途径是采用一种语言对图片库进行描述，其他语言到图片的翻译过程转化为先翻译成描述语言，再进行语言到图片的翻译。

##### parallel text

与dictionary相同，Language Grid提供的text，主要是多语言版的文件。

##### morphological analyzer

语义分析，对于用户输入的文本进行分词和词性标注。同样，用户可以选择不同的的analyzer进行分析，并将分析结果进行比对。

##### dependency parase analyzer

语义依存分析。与语义分析相同。

morphological analyzer和dependency parase analyzer与ltp做的事情比较相似。

##### translator

翻译器的服务提供机器翻译结果，用户可以选择源语言、目标语言和翻译系统。

#### Advanced

* dictionary creation
* parallel creation
* categorized word creation 这三项都需要登录才能进行操作。
* composite translation 将dictionary、parallel text结合起来进行翻译。
* document translation 针对文件结构特性，翻译的同时保留文件结构。

完整结果请点击<a href="http://blog.oneplus.info/nlp/langrid.html">这里</a>
