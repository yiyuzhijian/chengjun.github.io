---
layout: post
title: "建立一个并列的文本框"
date: 2015-02-23 17:41
comments: true
categories: 
- 博客
tags:
- 文本框
---

方法是设置position为absolute。

    #textbox {
      position:absolute;
      top: 200px;
      width: auto;
      margin-left: 50px;
      background-color: rgba(0,0,0,0.2);
      opacity:1;
    }

修改之后又觉得不好看。又尝试了iframe，也不是很合适。
