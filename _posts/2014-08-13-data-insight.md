---
layout: post
title: "数据洞察：掘地三尺的研究路径"
date: 2014-08-13 17:41
comments: true
categories: 
- blog
tags:
- 研究
- 数据
---


俗话说用志不分乃凝于神。最近有点分心，精力不集中，产生了很多问题。一个问题是计算士这边的活拉下来了。

###从异速增长率开始！

从异速增长率开始！It all starts with a big allowmetric growth rate! 异速增长率：这是一个重要的问题。比如一个流系统的节点是N， 产出是P,那么满足 $$P = N^\theta$$的关系。在互联网中，它就是PV和UV的关系。它提出了一个问题，即：为什么生物、城市、互联网都满足一个普世规律？它定量地表达了投入和产出的关系。

![](http://wiki.swarma.net/images/thumb/c/c5/Allowmetric_growht_digg_36_days.png/400px-Allowmetric_growht_digg_36_days.png)


为什么会有异速增长？一个可能的答案是流网络的自相似性。自己的哪里相似？究竟是什么地方？

引入耗散的视角：耗散阻碍了生长。每个小时里流网络而言，可以算每个节点i的耗散与流入。流入$$T_{i}$$和耗散$$D_{i}$$的差值就是节点i的流存量。

我们知道$$T_{i}$$和耗散$$D_{i}$$的关系同样满足一个标度规律。放在直角坐标系中，我们可以画出这种关系。

![](http://wiki.swarma.net/images/d/d9/Dissipation_digg_36_days.png)

直角坐标系隐含了一些潜在的假设：我们要按照从小到大的顺序（我称之为序假设，rank assumption）排列才能看到这种规律。坐标轴的作用就是这样。但要注意：流冰不是这样从耗散小的节点留到耗散大的节点。

###几何化

将流网络几何化，看成是一个由源向外的耗散。一个流网络，就可以算出任一节点到源头的流距离$$L_{i}$$。算法暂时省略。

整个网络按照半径重排：保持了网络的自相似性。

![](http://wiki.swarma.net/images/thumb/5/58/Hour23.png/400px-Hour23.png)






