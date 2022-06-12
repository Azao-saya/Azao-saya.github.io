---
title: 基本实体类包entity、model、vo、pojo都有什么区别
date: 2021-4-8 14:34:12 
categories: 云笔记
cover: https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/n.4nw88iqoshi0.jpg
---

 做项目的时候用到了这些看起来差不多的代码，总结确认一下它们的定义。

# Entity

数据表对应到实体类的映射，一个实体一张表，数据库进行交互做存储用途。

# Model

model是用于前端页面数据展示

model是一个高度优化组合或者精简后的一个用于在view层展示数据的对象。

比如存储时间的类型时，数据库中存的是**datetime**类型，entity获取的是**Date（）**类型，date类型的数据在前端展示的时候必须进行类型转换转为**String**类型。

所以在entity类型转换之后，存储到对应的model中，在后台做类型转换，然后将model传到前端显示时，前端就十分干净。

同时也可以添加字段，作为数据中转。

# Pojo

传统意义的java对象，最基本的Java Bean只有属性加上属性的get和set方法。

可以把POJO作为支持业务逻辑的协助类。

# Vo

value object值对象。POJO在表现层的体现。 当我们处理完数据时，需要展现时，这时传递到表现层的POJO就成了VO。它就是为了展现数据时用的。

# PO

POJO在持久层的体现，对POJO持久化后就成了PO。PO更多的是跟数据库设计层面相关，一般PO与数据表对应，一个PO就是对应数据表的一条记录。

# DAO

PO持久化到数据库是要进行相关的数据库操作的(CRUQ)，这些对数据库操作的方法会统一放到一个Java对象中，这就是DAO。

