---
layout: post
title: "去过的地方"
date: 2014-08-19 17:41
comments: true
categories: 
- 可视化
tags:
- 地图
- javascript
---

![](http://chengjun.qiniudn.com/Capture.PNG)

去看了下谷歌的[全球搜索可视化](http://data-arts.appspot.com/globe-search/)，感觉非常酷，它可以精确的展现精确的经纬度上的点的属性。接着找到了[chromeexperiments.com](http://www.chromeexperiments.com/globe)这个网页，列举了其它应用这个WebGL Globe的Javascript的可视化项目，其中一个是Github全球用户的可视化，源码见[这里](https://github.com/aaasen/github_globe)。

于是乎，我直接复制了gh-pages上的代码，然后上传到了自己的github。哎呀，读书人的事叫模仿，不叫偷。

我的想法是做一个自己到过的地方。

这里的数据格式非常简单，只要标定维度，经度，和数值就可以啦。

    var data = [
        [
        'seriesA', [ latitude, longitude, magnitude, latitude, longitude, magnitude, ... ]
        ],
        [
        'seriesB', [ latitude, longitude, magnitude, latitude, longitude, magnitude, ... ]
        ]
    ];

发现需要用最大值normalize这些magnitude。其中最大的值为1，会被显示为黄色。不错嘛！随便找个网站来定位城市的GPS地址：http://www.gps-coordinates.net/，找到我去过的城市：

- 兰州
- 北京
- 深圳
- 香港
- 长沙
- 新加坡
- 台湾
- 首尔
- 堪培拉
- 悉尼
- 凤凰城
- 西雅图
- 伦敦
- 阿姆斯特丹



效果[看这里](http://chengjun.github.io/globe/)

![](http://chengjun.qiniudn.com/traces.PNG)
