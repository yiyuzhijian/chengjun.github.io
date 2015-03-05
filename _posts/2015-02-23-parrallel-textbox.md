---
layout: post
title: "为网站首页添加消息框"
date: 2015-02-23 17:41
comments: true
categories: 
- 博客
tags:
- 文本框
---

我对于html的无知可以说是到了某种无以附加的程度。虽然我投入了很多时间，但往往都是干中学。而不是系统的模仿。通常会发现很多困惑，然后每次对我而言都是一个个小trick就解决了问题。

如何添加一个平行的文本框？这个困惑了我很久的问题，解决方法是设置position为absolute。

    #textbox {
      position:absolute;
      top: 200px;
      width: auto;
      margin-left: 50px;
      background-color: rgba(0,0,0,0.2);
      opacity:1;
    }

修改之后又觉得不好看。又尝试了iframe，也不是很合适。

之后发现一篇好文章[The Shapes of CSS](http://css-tricks.com/examples/ShapesOfCSS/).

修改了其中的talkbubble，放在application.css中。

    #talkbubble {
       position:absolute;
       top: 250px;
       margin-left: 50px;
       width: 300px;
       height: 150px;
       background-color: rgba(0,0,0,0.2);
       -moz-border-radius:    10px;
       -webkit-border-radius: 10px;
       border-radius:         10px;
    }
    #talkbubble:before {
       content:"";
       position: absolute;
       margin-left: 300px;
       top: 80px;
       width: 0;
       height: 0;
       background-color: transparent;
       #border-top: 5px solid transparent;
       border-bottom: 30px solid rgba(0,0,0,0.2);
       border-right: 120px solid transparent;
    }

在index.html里加入talkbubble来显示新闻。

    <div id="talkbubble">
      <h2><a href="http://chengjun.github.io/cv/news.html">News</a></h2>
      <p>[Feb 23] <a href="https://pypi.python.org/pypi/scholarNetwork/">scholarNetwork</a>--a python package which can help crawl and visualize the coauthor network of Google Scholar is released to Pypi. </p>
    </div>
