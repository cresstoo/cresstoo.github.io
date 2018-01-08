title: 用Highcharts制作特殊甘特图
date: 2014-05-09 13:32:32
tags: [highcharts, javascript]
---
### 关于Highcharts

[Highcharts][1]是一个纯正的JS图表库，内置了十几种图表，支持数组操作，从兼容性、可扩展性包括文档来看目前是最强大的免费图表库。研究了一段时间，不需要很多编程技巧也可以轻松做出动态图表来。
<!-- more -->

### 特殊甘特图的需求

手里有一个关于中国40年时间内真实通货膨胀系数的选题。除了需要用曲线图把通胀指数绘制出来，标示出40年间中国经济政策的主要管理者的人选变化，用甘特图来表示历届国家总理、央行行长、财政部长的人选和任期。

### 效果图（Excel制作）：

![Excel制作的甘特图][image-1]

用Highcharts来实现整个图表，有两个难点，一是任期变化的甘特图在Highcharts中并没有现成的例子，二是需要将上面的曲线图与下面的甘特图联动`mouse event`和`share tooltips`。
翻遍了官方论坛和stackoverflow，最后确定还是写一组函数来处理任期数据，比把任期数据写进data series更科学。

### 效果和代码如下：

{% jsfiddle ms4Xu result,js,html light 100% 300px %}

jsfiddle似乎被墙了，[请翻墙访问](http://jsfiddle.net/ms4Xu/light/)

[1]:	http://www.highcharts.com/

[image-1]:	http://duran.qiniudn.com/media/gantt.png