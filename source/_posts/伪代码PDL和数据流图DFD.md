---
title: 伪代码PDL、数据流图DFD、模块结构图
date: 2021-1-8 14:34:12 
categories: 云笔记
cover: https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/CX[D@T6{UF)YQJ8GR5XSGP1.2ztd9jthqia0.jpg
---


题目做到相关内容的，答案信息比较少没看出是个什么思路。查了伪代码是什么，网上的讨论都是十几年前的，也比较懵逼。

了解之后发现，虽然在编程前老老实实写伪码的很少。但类似效果的更加直观的流程图，PAD图还是经常有使用的。 <!--more-->

下面把题目贴上来:

## 画出对应的事务型数据流图(代码前数字只作标号用，不参与程序执行)

```
START
1:INPUT(A,B,C,D)
2:IF(A>0)AND(B>0)
THEN
3:X=A+B
ELSE
4:X=A-B
5:END
6:IF(C>A)OR(D<B)
7:Y=C-D
ELSE
8:Y=C+D
9:END
10:PPRINT(X,Y)
STOP
```

![](https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/QQ图片20210318162748.3j415j0uuui0.png)

用了亿图图示，连接线有点乱，总的来说就是一个自上而下的关系。

3和4，6和7是平级的关系选择一个进入下一步

因为是事务型数据流图，没有加别的信息，其实把IF、ELSE那些都写在旁边就一目了然了。

___

## 变换形数据流图&&模块结构图

![](https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/QQ图片20210318203620.2gczs9kd77fo.jpg)

上述图片为变换形数据流图，虚线是输入或输出与变换之间的界面

左侧第一条为输入与变换的界面，第二条为变换与输出的界面。

![](https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/asdas.4it6mr9vk2a0.png)

其实直线表示调用(简单起见，也可以用带箭头的线)，应该另起一条尾部空心圆的箭头线来传递数据信息(尾部为实心圆为控制信息)，图中无控制信息。

![](https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/QQ图片20210318230239.2twaixpc88s0.jpg)

原谅字丑，这应该是完整的。感觉软件整不明白还是手写了。

题目中写了用圆十字表示或者，但没打印出来我查了别的资料是在g1和g2上有这个符号。

A1调用A2和A3是通过一个多出来的菱形连接的，表示条件调用。应该也可以多调用一个判断模块来完成条件调用。

这些东西其实资料不是很多，答案也都怪怪的，没人教我只能尽量自己思考脑补，如果错了希望能告诉我。