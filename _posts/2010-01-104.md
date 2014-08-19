---
layout: post
title: "3D地球可视化：WebGL Globe"
date: 2014-08-19 17:41
comments: true
categories: 
- 可视化
tags:
- 地图
---

去看了下谷歌的[全球搜索可视化](http://data-arts.appspot.com/globe-search/)，感觉非常酷，它可以精确的展现精确的经纬度上的点的属性。

接着找到了[chromeexperiments.com](http://www.chromeexperiments.com/globe)这个网页，列举了其它应用这个WebGL Globe的Javascript的可视化项目，其中一个是Github全球用户的可视化，源码见[这里](https://github.com/aaasen/github_globe)。

于是乎，我直接复制了gh-pages上的代码，然后上传到了自己的github。哎呀，读书人的是叫模仿，不叫偷。

我的想法是做一个自己到过的地方。

  var data = [
      [
      'seriesA', [ latitude, longitude, magnitude, latitude, longitude, magnitude, ... ]
      ],
      [
      'seriesB', [ latitude, longitude, magnitude, latitude, longitude, magnitude, ... ]
      ]
  ];

