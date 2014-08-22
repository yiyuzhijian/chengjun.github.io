---
layout: post
title: "生活的细节：行走在2014年"
date: 2014-05-04
comments: true
categories: 
- 生活
tags:
- 工作
---


#### 大学的尾巴

转眼之间，大学到了尾巴上。我习惯于拖拉，终于使得自己也尝到了恶果。于是，想着要灌几篇水文。我觉得自己的运气说不上好，追求的一些东西，最终多没有什么让我满意的成果出来。慢慢地对自己充满了厌恶。乐天知命多是托词。混吃等死才是生活。这不是我预料到。不过，暂时也只能这么样了。

2014-05-08
今天又被老板追着要论文修改结果，我匆匆忙忙把摘要改了一遍发了过去。真心觉得自己在英语方面的进步不大。实在是非常惭愧。以后一定要积极主动些。不要让别人催自己，都是我自己的事情，为什么要别人来催呢。


昨天晚上面了马里兰大学的博后，原来他主要想让我过去做文本挖掘。有趣。看来只是一个项目而已。这就是生存的层面了。

![](http://upload.wikimedia.org/wikipedia/en/thumb/0/07/Lifetitle.jpg/250px-Lifetitle.jpg)


2014-06-23

琢磨出一个不用每次在jekyll上写博客都要上传的方法：将要显示的博客的categories设为blog，一次上传n个草稿（不指定categories），使用liquid语言指定在博客列表中只显示blog类的。这样草稿不会被显示，每次在线登录github，更改一个草稿的标题和categories就可以了。图片用外链flickr。

今天下午鼓捣了半天jekyll的设置，最初是想弄一个[paginator](http://jekyllrb.com/docs/pagination/)给文章列表分页，结果搞了半天，没搞定。各种问题。[Patrick McKinley](http://patrick-mckinley.com/tech/jekyll-pagination.html)说是因为不是网站第一层的index.html，所以jekyll官方设置时没有用的。于是，直接用他的方法，发现没有办法在我的网站上实现。

Patrick McKinley的博客以图片来显示博客文章的方法似乎很酷。感兴趣，去研究了下他的[代码](https://github.com/lilmuckers/lilmuckers.github.com)，大致是设置了post.image，图片存放在assets中的图片文件夹。我弄了下，也没弄成功。

又看到[Mr Trường at RMIT](tmtxt.github.com)的网页，翻了半天，加了related_posts功能。 


没想到晚上更惨，被python的encoding error搞得很头大！
