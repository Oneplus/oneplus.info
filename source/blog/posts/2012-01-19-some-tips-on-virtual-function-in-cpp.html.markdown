---
layout: post
status: publish
published: true
title: C++笔记 - 虚函数几个小问题
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "#### 问题零：虚函数与纯虚函数有什么区别\r\n<li>定义一个函数为虚函数，不代表函数为不被实现的函数。定义他为虚函数是为了允许用基类的指针来调用子类的这个函数。</li>\r\n<li>定义一个函数为纯虚函数，才代表函数没有被实现。定义他是为了实现一个接口，起到一个规范的作用，规范继承这个。类的程序员必须实现这个函数。</li>\r\n（上面这段转载自<a
  href=\"http://www.cppblog.com/ElliottZC/archive/2007/07/20/28417.html\">这里</a>，我觉得解释得非常清楚）\r\n\r\n"
wordpress_id: 388
wordpress_url: http://blog.oneplus.info/?p=388
date: 2012-01-19 16:09:33.000000000 +08:00
categories:
- 可以控制
- 挨踢民工
tags:
- C++
comments:
- id: 417
  author: ronaflx
  author_email: 900831flx@gmail.com
  author_url: ''
  date: !binary |-
    MjAxMi0wMS0yNSAyMjoyMTo0OSArMDgwMA==
  date_gmt: !binary |-
    MjAxMi0wMS0yNSAxNDoyMTo0OSArMDgwMA==
  content: ! "关于问题3\r\n其实我觉得这是一个很优秀的地方……\r\n防止了产生的很多问题，当然反面就是不灵活.\r\n我个人比较赞成这样的代码给出编译错误"
- id: 474
  author: Shiina Luce
  author_email: zxteloiv@gmail.com
  author_url: http://liselsia.org
  date: !binary |-
    MjAxMi0wMi0xNSAxMjoxNDoxNyArMDgwMA==
  date_gmt: !binary |-
    MjAxMi0wMi0xNSAwNDoxNDoxNyArMDgwMA==
  content: ! "豆瓣党特来一拜……\r\n抽象类这么规定是有它的考虑，基本上它也只建议被当作java的接口的类似东西来用。即使抽象类中有实现的东西，也不推荐放到抽象类里（而放到它的基类中去）：\r\nclass
    AbstractClass { ... blablabla ... };\r\nclass MyInterface : public AbstractClass
    {\r\npublic:\r\n    virtual foo1() = 0;\r\n    virtual foo2() = 0;\r\n};\r\n这样拿到你的库的人只需要include接口的头文件就行，这算是一种封装和设计的意义吧。"
---
#### 问题零：虚函数与纯虚函数有什么区别

* 定义一个函数为虚函数，不代表函数为不被实现的函数。定义他为虚函数是为了允许用基类的指针来调用子类的这个函数。
* 定义一个函数为纯虚函数，才代表函数没有被实现。定义他是为了实现一个接口，起到一个规范的作用，规范继承这个。类的程序员必须实现这个函数。

（上面这段转载自<a href="http://www.cppblog.com/ElliottZC/archive/2007/07/20/28417.html">这里</a>，我觉得解释得非常清楚）

#### 问题一：抽象类的析构函数可以是纯虚函数吗

答案是可以的。通过纯虚析构函数，可以防止抽象类被实例化。但是，这里有一个逻辑上的矛盾。由于抽象类往往与具体类对应，从类的继承关系来看，抽象类往往是某些类的基类，如果有继承关系存在，派生类就需要知道基类的析构函数。所以，类似于

~~~cpp
class fruit {
public:
    fruit() {}
    //virtual ~fruit() = 0;
    virtual ~fruit() { cout << "deallocate fruit." << endl; }
    virtual void taste() = 0;
};

class apple : public fruit {
public:
    apple(const char *_name) : name(_name) {}
    ~apple() { cout << "deallocate apple." << endl;}

    void taste() {
        cout << "apple [" << name
            << "] is rich of juice." << endl;
    }

    void smell() {
        cout << "apple [" << name
            << "] smells good." << endl;
    }

    const char *name;
};
~~~

的代码不能编译通过。

#### 问题二：如何将同一抽象类的若干子类的实例用同一结构存储

<img height="250" src="http://blog.oneplus.info/wp-content/uploads/2012/01/g1.png">

假设已经有如同图的设计，现在想用一个vector或者数组将不同种的fruit存储在一起。但是，抽象类不能实例化，所以，类似于`vector<fruit> fruits;`或者`fruit *fruits = new fruit[3];`
的代码都是不能编译通过的。不过，虽然`fruit *fruits = new fruit[3]`不能编译通过，`fruit *fruits = (fruit *)calloc(3, sizeof(fruit));`这样的C风格的代码却可以编译通过。只是在运行过程中，一旦调用fruit子类的方法就会出现segment fault。要分析上面问题的原因，就要简单解释一下C++虚函数的实现方法。

在没有C++时，C程序员可以在结构体中保存函数指针的方法来实现一些简单的重写(override)，比如一个链表，喜欢面向对象的程序员或许会把它写成：

~~~c
typedef struct _list_node node_t;
typedef struct _list      list_t;

struct _list_node {
    int data;
    node_t *next;
};

struct _list {
    node_t *head;

    void (*init)(list_t *list);
    void (*append)(list_t *list, int data);
};
~~~

然后定义一些不同的append的方式把list->append的函数指针指向这些函数名，也从一定程度上实现了面向对象中的封装。

而C++对于函数的实现思路与上面大致类似。对于每个类都保存一组函数指针的表。在发生类的继承关系后，由编译器处理各函数指针指向的函数入口。在调用成员函数时，通过这个表找到对应函数的入口地址。对于这段代码：

~~~cpp
fruit *fruits = (fruit *)calloc(3, sizeof(fruit));
fruits[0] = apple("ipad");
fruits[1] = banana("what");

for (int i = 0; i < 2; ++ i) {
    (fruits + i)->taste();
}
~~~

用VS2008调试，发现fruits变量所指向的内存中，__vfptr(是前面提到的虚指针)的值为0，也就是在调用taste方法时，找不到正确的函数入口，所以出现了segment fault。

这个实例从另一个角度也说明，C++的new关键字并非只做分配内存的工作。再进一步就是，C++程序中尽量不要出现C风格的内存分配，百害而无一益。

回到最初讨论的问题，要实现同一抽象类的若干子类的实例用同一结构存储，一种可行的方法是保存fruit类的指针。将代码变为：`vector<fruit *> fruits;`或者`fruit **fruits = new fruit *[3];`

#### 问题三：能否通过抽象类的指针访问具体类中的某些未在抽象类中声明的函数

这个，显然是不能的。比方说，如下代码

~~~cpp
fruit *app = new apple();
app->smell();
~~~

编译不过。这也是我觉得C/C++相对于动态语言非常不灵活的一方面。
