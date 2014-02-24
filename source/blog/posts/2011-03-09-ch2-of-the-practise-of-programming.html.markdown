---
layout: post
status: publish
published: true
title: 程序设计实践一 - 第二课
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "<script src=\"http://ajax.googleapis.com/ajax/libs/jquery/1.5/jquery.min.js\"></script>\r\n<script
  type=\"text/javascript\">\t\t\r\n$(document).ready(function(){\r\n$(\".text\").toggle();\r\n$(\".box\").toggle(function(){\r\n$(this).next(\".text\").animate({height:
  'toggle', opacity: 'toggle'}, \"slow\");\r\n} ,function() {$(this).next(\".text\").animate({height:
  'toggle', opacity: 'toggle'}, \"slow\");});});</script>\r\n### 课程提纲\r\n<div
  class=\"box\">请点击<a href=\"#\">这里</a></div>\r\n<div class=\"text\">\r\n* 上节课的回归与作业讲解\r\n* 分治\r\n* 二分算法\r\n\r\n
  \   * 例一：求x=&radic;9.8\r\n    \r\n\t\t* 题目描述\r\n        * 算法过程演示\r\n
  \       * 算法分析\r\n        * 伪代码与代码\r\n    \r\n\t* 例二：二分查找\r\n\t\r\n
  \       * 题目描述\r\n        * 题目分析\r\n        * 伪代码与代码\r\n        * 复杂度分析\r\n
  \   \r\n\t* 讨论：整数二分的最好写法\r\n\t\r\n        * 例一\r\n        * 例二\r\n
  \   \r\n\t* 例三：求一列有序数中第一个大于等于某数的数\r\n\t\r\n        * 题目描述\r\n
  \       * 题目分析\r\n        * 伪代码与代码\r\n        * 拓展：最大化最小/最小化最大的一般分析方法\r\n
  \   \r\n\t* 教你偷懒：lower_bound、upper_bound\r\n\r\n* 堆\r\n\r\n
  \   * 离线算法与在线算法\r\n    * 引例：只有添加操作的在线求一列数的最大值\r\n\t\r\n\t\t* 题目描述\r\n
  \       * 题目分析\r\n    \r\n\t* 例四：支持添加和删除最大操作的在线求一列数的最大值\r\n\t\r\n\t\t* 题目描述\r\n
  \       * 算法一\r\n        * 算法二\r\n        * 总结算法一二的悲剧之处\r\n
  \   \r\n\t* 堆的性质\r\n    * 堆的操作\r\n    \r\n        * 上浮\r\n
  \       * 下沉\r\n        * 删除最大\r\n        * 添加\r\n    \r\n\t* 伪代码与代码\r\n
  \   * 教你偷懒：priority_queue\r\n\r\n\r\n</div>\r\n### 简单的讲义\r\n"
wordpress_id: 125
wordpress_url: http://blog.oneplus.info/?p=125
date: 2011-03-09 08:03:05.000000000 +08:00
categories:
- 可以控制
- HIT ACM/ICPC Group
- 程序设计实践
tags:
- ACM Group
- 程序设计实践
- 哈尔滨公交系统
comments:
- id: 54
  author: zxdhuge
  author_email: zxdhuge@gmail.com
  author_url: http://zxdhuge.com
  date: !binary |-
    MjAxMS0wMy0wOSAxOTowMDoxOSArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0wOSAxMTowMDoxOSArMDgwMA==
  content: hello world  ^_^
- id: 55
  author: Oneplus
  author_email: oneplus.lau@gmail.com
  author_url: http://blog.oneplus.info
  date: !binary |-
    MjAxMS0wMy0xMCAwODowMDowNSArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0xMCAwMDowMDowNSArMDgwMA==
  content: 小东，已经加友链了~
- id: 56
  author: noname
  author_email: jerrybond6@126.com
  author_url: ''
  date: !binary |-
    MjAxMS0wMy0xMSAxODoyMToyMCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0xMSAxMDoyMToyMCArMDgwMA==
  content: 你真是太牛B了
- id: 57
  author: jerrybond6
  author_email: jerrybond6@126.com
  author_url: ''
  date: !binary |-
    MjAxMS0wMy0xMSAxODoyMjoxMCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0xMSAxMDoyMjoxMCArMDgwMA==
  content: 你真是太牛B了 不解释
---

### 课程提纲

* 上节课的回归与作业讲解
* 分治
* 二分算法
    * 例一：求x=&radic;9.8
        * 题目描述
        * 算法过程演示
        * 算法分析
        * 伪代码与代码
    * 例二：二分查找
        * 题目描述
        * 题目分析
        * 伪代码与代码
        * 复杂度分析
    * 讨论：整数二分的最好写法
        * 例一
        * 例二
    * 例三：求一列有序数中第一个大于等于某数的数
        * 题目描述
        * 题目分析
        * 伪代码与代码
        * 拓展：最大化最小/最小化最大的一般分析方法
    * 教你偷懒：lower_bound、upper_bound
* 堆
    * 离线算法与在线算法
    * 引例：只有添加操作的在线求一列数的最大值
        * 题目描述
        * 题目分析
    * 例四：支持添加和删除最大操作的在线求一列数的最大值
        * 题目描述
        * 算法一
        * 算法二
        * 总结算法一二的悲剧之处
    * 堆的性质
    * 堆的操作
        * 上浮
        * 下沉
        * 删除最大
        * 添加
    * 伪代码与代码
    * 教你偷懒：priority_queue

### 简单的讲义

讲义请看<a href="http://acm.hit.edu.cn/~oneplus/design-2011/02-lecture.pdf">这里</a><br />

PPT请看<a href="http://acm.hit.edu.cn/~oneplus/design-2011/02-ppt.pdf">这里</a>

### 录了30多分钟的课堂录音

这节课是用自己的笔记本进行的演示，录到了课堂录音。原文件噪音非常多，用Goldwave处理了一下，果然好了不少。
<embed src="http://acm.hit.edu.cn/~oneplus/design-2011/02-record.wma" autostart="false"></embed>

### 自我检讨

* 因为课程录了音，所以对于自己的授课内容有了一个比较清楚的认知。
* 从这节课的录音来看，我讲课的一些问题包括：重复冗余严重，二分的算法过程被说了三次、二分复杂度证明说了两次；语气平淡，重点不突出；声音比较小，有点无力。
* 而且这节课在多媒体的问题上花的时间有点多。大概有十五分钟都是在调多媒体…
* 自己笔记本的时间和8503机器的时间不同步，在课间休息时间的问题上把握得不好。
* 现在看，自己的讲义是挺混乱的。课件做得尤其糟糕。
* 这里需要向上课的同学道歉，第二课我的准备工作的确有不足。这节课的准备中，把太多时间花在demo上，以至于没有足够的时间去思考要讲什么内容。下节课demo的东西比较少，我会认真准备课程内容的。


### 浮云一样的heap的demo

其实这个flash动画也是我做的…

### 演示二分时用的Java代码

~~~java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.awt.Panel;
import java.io.*;
import java.text.DecimalFormat;

public class bisearch extends JFrame implements ActionListener {
    public bisearch() {
        setLayout(new FlowLayout(FlowLayout.LEFT));
        setSize(500, 400);
        setBackground(Color.white);
        
        nextButton = new Button( "Next" );
        nextButton.addActionListener( this );
        add( nextButton );
        
        init();
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
    
    public void init() {
        lowerBound = f( leftBound );
        upperBound = f( rightBound );
        low = 3.0;
        high = 4.0;
        //System.out.println( lowerBound + " " + upperBound );
    }
    
     public void paint( Graphics g ) {
         point p1 = new point();
         point p2 = new point();
         p1 = toPoint(2.7, 0.0 );
         p2 = toPoint(4.3, 0.0 );
         x_axis = p1.getY();
         g.drawLine( p1.getX(), p1.getY(), p2.getX(), p2.getY());
        g.drawLine( 40, 0, 40, 400);
        g.drawString( "y axis", 35, 75 );
        g.drawString( "x axis", 450, x_axis );
         
         for( double i = leftBound; i <= rightBound; i = i + eps ) {
             double x = i, xx = i + eps;
             double y = f( x ), yy = f( xx );
             
             p1 = toPoint( x , y );
             g.drawLine( p1.getX(), p1.getY(), p1.getX(), p1.getY());
         }
         p1 = toPoint( 3.0, f(3.0) );
         p2 = toPoint( 4.0, f(4.0) );
         g.drawOval( p1.getX() - 3, p1.getY() - 3, 6, 6);
         g.drawOval( p2.getX() - 3, p2.getY() - 3, 6, 6);
         g.drawLine( p1.getX(), p1.getY(), p1.getX(), x_axis );
         g.drawLine( p2.getX(), p2.getY(), p2.getX(), x_axis );
         new DecimalFormat( "0.00" );
         g.drawString( Double.toString( 3.0 ), p1.getX(), x_axis + 12);
         g.drawString( Double.toString( 4.0 ), p2.getX(), x_axis + 12);
         //System.out.println( p1.getX() + " " + p1.getY() );
    }
     
    public double f( double x ) {
        return x * x - 9.8;
    }
    
    public point toPoint( double x, double y ) {
        double xx = ( x - leftBound ) / ( rightBound - leftBound ) * 500.0;
        double yy = ( y - upperBound ) / ( lowerBound - upperBound ) * 400.0;
        
        point ret = new point( (int)xx , (int)yy );
        return ret;
    }
    
    public void actionPerformed( ActionEvent event ) {
        if( event.getSource() == nextButton ) {
            if( high - low > 0.001 ) {
                mid = ( low + high ) * 0.5;
                new DecimalFormat( "0.00" );
                point p1 = toPoint( mid, f(mid) );
                getGraphics().drawOval( p1.getX() - 3, p1.getY() - 3, 6, 6);
                getGraphics().drawLine( p1.getX(), p1.getY(), p1.getX(), x_axis );
                 getGraphics().drawString( Double.toString( mid ), p1.getX(), x_axis + 12);
                double tmp = f( mid );
                if( f( mid ) > 0 ) {
                    high = mid;
                }
                else {
                    low = mid;
                }
            }
        }
    }
    
    public static void main(String[] args) throws IOException {
        bisearch bs = new bisearch();
        bs.setVisible(true);
    }
    
    private double low, high, mid;
    private double leftBound = 2.7, rightBound = 4.3, eps = 0.003;
    private double lowerBound, upperBound;
    private int x_axis, y_axis;
    Button nextButton;
}

class point {
    public point() {
        x = 0;
        y = 0;
    }
    public point(int _x, int _y) {
        x = _x;
        y = _y;
    }
    public int getX() { return x; }
    public int getY() { return y; }
    private int x;
    private int y;
}
~~~

太懒，不想把这段代码弄成applet了，想看编译后结果的同学点击<a href="http://acm.hit.edu.cn/~oneplus/design-2011/02-bisearch.jar">这里</a>下载可执行程序啊。

### 杂碎

* cai组队的事纠结了。
* 84路换车站了，昨天从教化桥的一头跑到另一头去坐公交，T.T。以后再也不坐84了。
* 上周的大概把三天时间花在toolbox源码的调研上，到周日才搞清楚要做的应该是service grid。脑残了…
* 事情太多，还需多多努力啊…

