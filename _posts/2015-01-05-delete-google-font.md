---
layout: post
title: "挥泪斩谷歌字体"
date: 2015-01-05 22:41
comments: true
categories: 
- blog
tags:
- 谷歌
- 字体
---


俺天朝跟谷歌成了死敌。背后的很多想法让人很无奈。虽然米果是两党制，但是谷歌据说也在检查之列。到了俺朝，美利坚放不下身段了，天朝也放不下，于是就僵住了。于是很多谷歌的服务都不好用了。比如谷歌学术，谷歌邮箱。哎妈呀，老伤心老。我这里要说的却是谷歌的字体格式。


###谷歌字体
在天朝载入我的博客慢的原因就是因为style.css里（media/css/style.css）调用里谷歌字体。好伤心，每次访问速度都很慢，非得翻墙才行。可是不能让俺的读者们也翻墙吧，这也太虎了。反正我的审美要求也没那么高。雪藏了吧。


    #@import url(http://fonts.googleapis.com/css?family=Galdeano);
    #@import url(http://fonts.googleapis.com/css?family=Electrolize);
    #@import url(http://fonts.googleapis.com/css?family=Cuprum);

###改过来之后
我了个去，怎么英文字体变这么大了，BIG好吧，只能骗自己感觉萌萌哒啦。

###把谷歌字体放在本站
其实很早就注意到andy wang的这个解决方法，一直比较懒。还是去在mac上安装了github for mac，于是把andy wang的media文件夹偷到我这里来用。

Andy Wang:
`你好，我扒走了你的模板，然后在天朝用发现非常慢，然后调试了一下，发现是在style.css和home.css里面有从别的网站下载字体文件的, http://fonts.googleapis.com/这个网站在天朝访问非常不稳定，所以做了一些小改动，把字体文件都下载到网站上了，页面渲染速度也快了很多。https://github.com/synckey/synckey.github.io/tree/master/media/css`

终于，世界再次变得一片清凉了。真好。






