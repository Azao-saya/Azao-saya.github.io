---
title: Hello Sheleterz
date: 2021/6/3 20:46:25
categories: 折腾
tags:
- 博客
- Hexo
top: 9
cover: /images/Lq7IbZTiEr68jMD.c0v39875irs.jpg
---

本站建站于2019年9月，流下了没有技术只能当一个的无情的做题家的泪水。

最近才算把博客各种窟窿堵上(还有剩下..)(全部堵上了)

至此终于能说上我有自己的博客了，也总结一下用到了哪些东西

<!--more-->

## 博客框架

**Hexo**

## 主机

**Github Pages**（已弃用）

**Gitee Pages**（无法使用自定义域名放弃，体感是访问最快的）

**Coding Pages**（访问速度过慢...弃用）

**Github Pages+Vercel**（目前）：兜兜转转还是回到这里，Vercel使用了Amazon Global Accelerator AGA网络用来加速站点国内访问。https://luotianyi.vc/4801.html

上面文章中的博主是用反向代理二级域名作为中间层转发间接访问主域名，我自己则是把二级域名反向代理在Vercel，同时直接连接Github项目把主域名部署在Vercel。

可能搞错了什么，但以香港节点进行的测试的话网站性能极佳。

![](https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/QQ图片20210120143557.2lhpncbf5d20.png)

![](https://cdn.jsdelivr.net/gh/Azao-saya/image-blog@master/20210102/QQ图片20210120143835.2zu95zm64zg0.png)

## 主题

nexmoe: https://github.com/theme-nexmoe/hexo-theme-nexmoe

## 评论

使用了一段时间**Gitalk**

初始化麻烦后弃用

更换为**Valine**：https://valine.js.org/

评论系统放在**Leancloud**：https://www.leancloud.cn/

尚未使用**Valine-Admin**，卡在备案的域名上，所以瞎了。

需要和我联系最好用主页上提供的任意联系方式，或者评论在关于我上随缘交流。

听说已有**valine**的上位替代**waline**了，直观感受到了学到死的现状。

————————————

已替换为waline，评论会通过邮件服务器告知我，如果有回复评论者也会同样知道。

## 图床

最开始使用**SM.MS**配合**Quicker**的插件一键上传图片，有被方便到。

后发现加载速度很慢，便从别人博客偷师，发现图片地址带了**jsDelivr** 

找上了**PicX**， 基于 **GitHub** 的图床神器，使用 **jsDeliv**r 进行 CDN 加速 

需要注意的是如果图片文件名称的字符过于离奇会导致无法上传，上传中发有图片歧视后尝试更改名称解决。

目前使用图片已全部迁移

------------

jsdeliver备案许可被注销，国内访问已被污染，目前把首页的图片直接在本地存储了，正在考虑其他解决办法....

## 图标

**iconfont**

## 加了什么

**插件:**

**hexo-renderer-kramed:** https://github.com/sun11/hexo-renderer-kramed

**hexo-renderer-mathjax :** https://github.com/phoenixcw/hexo-renderer-mathjax

> 文章中使用了LaTeX公式，Hexo默认不支持并和markwon语义存在冲突，安装后需要更改配置
>
> 需要注意title: 我是标题 date: 2020-08-15 23:18:50 tags: mathjax: true
>
> 文章中也要开启mathjax: true

**hexo-generator-index-pin-top**：https://github.com/netcan/hexo-generator-index-pin-top

> 实现博客置顶

**avatarRotateZ** ：头像旋转，配上我自己的头像感觉挺可爱的

**hexo-generator-json-content:** https://github.com/alexbruno/hexo-generator-json-content

> 实现站内搜索

**hexo-tag-aplayer**：https://github.com/MoePlayer/hexo-tag-aplayer：

> 音乐播放器

**hexo-deployer-git：**https://github.com/hexojs/hexo-deployer-git

> Git 部署器

**不知道叫啥**： 当博客为不活跃标签页时，更换站点标题为

> “我在这呢 大于等于 欧米伽 小于等于”



本来还有很多花里胡哨的感觉会拖累网站性能还是删除了

