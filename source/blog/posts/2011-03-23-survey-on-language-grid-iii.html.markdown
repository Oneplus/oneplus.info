---
layout: post
status: publish
published: true
title: Language Grid调研结果[iii]{补作业完结篇+番外篇}
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "<div id=\"architecture\">\r\n#### Language Grid的设计结构如图\r\n\r\n"
wordpress_id: 142
wordpress_url: http://blog.oneplus.info/?p=142
date: 2011-03-23 19:34:06.000000000 +08:00
categories:
- 可以控制
- HIT CIR
- Language Grid调研
tags:
- CIR
- Language Grid
comments:
- id: 70
  author: kinslover
  author_email: kinslover@gmail.com
  author_url: http://kinslover.info
  date: !binary |-
    MjAxMS0wMy0yNCAxMjoyNzozMyArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0yNCAwNDoyNzozMyArMDgwMA==
  content: 沙发，太令人膜拜了！
- id: 100
  author: darkgt
  author_email: darkgt@163.com
  author_url: ''
  date: !binary |-
    MjAxMS0wNC0xMSAxMjowMzo1OSArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNC0xMSAwNDowMzo1OSArMDgwMA==
  content: 图是用啥画的？
- id: 102
  author: Oneplus
  author_email: oneplus.lau@gmail.com
  author_url: http://blog.oneplus.info
  date: !binary |-
    MjAxMS0wNC0xMSAxMjowOTowMiArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNC0xMSAwNDowOTowMiArMDgwMA==
  content: ! "edraw mindmap 土鳖软件\r\nvisio好像比较强大。"
---
#### Language Grid的设计结构如图

其中，Core Node是Language Grid的核心节点，用于保存Service的一些信息。Service之间的相互调用，需要经过Core Node。Wrapper是Language Grid面向语言服务的一种Service。主要用于与语言资源、软件API交互。应用用户在调用Language Grid提供的语言服务时，需要经过Core Node访问Wrapper。Language Grid网站上提供的Language Grid可以看作是一种Wrapper。

![structure](http://blog.oneplus.info/wp-content/uploads/2011/03/2-1.png)

Service Grid的层次可以看做

![grid](http://blog.oneplus.info/wp-content/uploads/2011/03/2-2.png)

三个层次的作用分别是

* Service
    * 与Web Request、Application Request交互
    * 与Program、Language Resource交互
    * Service一方面是接受应用请求，另一方面是调用语言资源。
* Grid
    * 工作在DB与Service之间，提供DB的接口给Service
    * 另一点作用是与其他Grid进行交互
* Service DB
    * 保存Grid、Service的ID、url等属性

### 三个层次的通信方式

* Web Request to Service : HTML ; Application Request to Service : SOAP
* Service to DB : java.dao(由于Grid只是一个中间介质，在源码中没有实体化的描述)

### Service调研

![service](http://blog.oneplus.info/wp-content/uploads/2011/03/2-3.png)

各个模块的作用

#### Service Manager

用于添加、删除、修改Service在DB中的信息。是Service层和Grid层的交互接口

#### Service Supervisor

控制访问权限

#### Composite Service

用于用户查找、部署Service。举例解释其作用，如果有一个Translate命令输入，Service Grid会先通过Composite Service找到相符的Translation Service。然后再进行与Atomic Service的交互。

#### Atomic Service

用于保存Wrapper、与Resources、API交互。是Service Grid服务的外部接口。

#### 各模块之间通信方式

* Service Supervisor to Composite/Atomic Service : SOAP, Java Method
* Composite Service to Service Supervisor : SOAP, Java Method
* Atomic Service to Resource : WSDL

### Atomic Service的调研

Atomic Service完成一些Service Grid和语言资源、软件API的交互，是Service Grid最靠外的一层。Atomic Service的方法由AbstractSerive及其子类描述。其中包括AbstractAdjacencyPairService、AbstractMorphologicalAnalysisService等。

其中，类的继承关系如下

~~~java
AbstractService
	AbstractLanguageService
		AbstractAdjacencyPairService // 机器问答
		AbstractConceptDictionaryService // 概念词典
		AbstractDependencyParserService // 依存分析
		AbstractLanguageIdentificationService 
		AbstractMorphologicalAnalysisService // 词性分析
		AbstractParaphraseService
		AbstractPictogramDictionaryService
		AbstractSimilarityCalculationService
		AbstractSpeechRecognitionService
		AbstractTemplateParallelTextService
	AbstractLanguagePairService
		AbstractBilingualDictionaryService 
		AbstractDictionaryService
		AbstractParallelTextService
		AbstractTranslationService
~~~

对于上述AbstractService，Service Grid源码中不提供该项服务的解决方案，而是要求通过重载运算来实机器问答、机器翻译等功能。

各项AbstractService提供重载的接口如下

* AbstractAdjacencyPairService
    * 接口:search(String category, String Language, String firstTurn, String matchingMethod)
    * 重载:doSearch(String category, Language Language, String firstTurn, MatchingMethod matchingMethod)
    * 预处理:无
* AbstractConceptDictionaryService
    * 接口:searchConcepts(String language, String word, String matchingMethod)
    * 接口:getRelatedConcepts(String language, String conceptId, String relation)
    * 重载:doSearchConcepts(Language language, String word, MatchingMethod matchingMethod)
    * 重载:doGetRelatedConcepts(Language language, String conceptId, ConceptualRelation relation)
    * 预处理:无
* AbstractParalledlTextService
    * 接口:search(String sourceLang, String targetLang, String source, Stirng matchingMethod)
    * 重载:doSearch(Language sourceLang, Language targetLang, String source, MatchingMethod matchingMethod)
    * 预处理:无
* AbstractDependencyParserService
    * 接口:parseDenpendency(String language, String sentence)
    * 重载:doParseDependency(Language language, String sentence)
    * 预处理:无
* AbstractMorphologicalAnalysisService
    * 接口:analyze(String language, String text)
    * 重载:doAnalyze(Language language, String text)
    * 预处理:无
* AbstractTranslateService
    * 接口:translate(String sourceLang, String targetLang, String source)
    * 重载:doTranslate(Language sourceLang, Language targetLang, String source)
    * 预处理:invokeDoTranslate
        * 将待翻译文本分成{'NONE', 'WORD', 'FULL', 'FULL_WITH_PUNCTUATION'}四种，进行预处理
        * NONE直接翻译
        * WORD按截止符拆分成单段，再调用单个词翻译
        * FULL按截止符拆分成单段，再调用多个词同时翻译

经过两个星期的调研，我个人对于Service Grid的理解是，相比语言服务，Service Grid提供的更多是一种一套语言服务系统。对于提供怎样的翻译，怎样的依存分析，Service Grid并不关心。其关心的重点是，如何在翻译的请求到来时，调用各个Wrapper的翻译功能。而最初看到的将多种语言服务结合使用，在Service Grid的源码中没有体现，应该也是Wrapper通过重载方法实现的。
<del>调研过程到这里就太监了</del>

<div>_______________________我是番外篇的分割线________________________</div>

总结这次调研工作

1. 平生第一次读60M的代码（实际上大概读了其中的20%）
2. 像Language Grid这种思路是不是就是所谓的面向服务的软件设计呢
3. 软件调研，要从Manual下手。在真正开始看代码之前，要认真阅读Manual，甚至来讲，Manual要比真正的代码还重要。因为，软件的开发者会清晰地描述他们的设计思路，而这方面上Manual远比代码直接。开始读Java源码之前，还把三天时间放在Toolbox上面了，如果早点读Manual，或许会少走不少弯路。
4. 如果以后参与开发，也要认真写好Manual，这个无论对于自己还是对于他人都是有好处的。

整个这个工作在上个星期时已经结束了，但是一直没拿出时间来把这篇总结写出来，也不知道自己都在做些啥。摔！

