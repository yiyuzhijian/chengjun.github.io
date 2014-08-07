---
layout: post
title: "可视化比赛"
date: 2014-07-21 17:41
comments: true
categories: 
- blog
tags:
- 
---


现有数据有学校信息。我可以通过构建字典的方式来将user_id和学校信息（以最新的学校信息为主）剥离出来。使用这个字典可以计算学校人数的分布并挑选前一百的学校。然后根据user_id来match社交网络数据和学校数据，构建：university1---university2---date的数据形式。如果该行数据中的学校都在top100的名单中，则保留，否则不保留，这样可以构建所需要的学校和学校的随时间变化的网络。可以用户社区划分等方面。动态网络的展现可以参考这个作品：


我是想通过这个图从一个侧面说明各个大学在社交网络上的影响力和关系：所以节点大小表示每个大学在该网络中的人数，连边宽度表示节点之间的连接关系，节点颜色的不同可以表示节点的影响力大小（中心性指标）。


    library(igraph)
    setwd("F:/xiaonei/")
    
    ################
    # all data
    ################
    data = read.table("./friends_university_top100_by_all.txt", header = FALSE, 
                     sep = '\t', stringsAsFactors = FALSE)
    #g =graph.data.frame(data[,1:2],directed=FALSE )
    #E(g)$weight = data[,3]
    # a = which(rank(-graph.strength(g)) <= 50)
    
    data = data[which(data[,3] >= mean(data[,3])*1.2), ]
    data = data[which(data[,1] != data[,2]),]
    g =graph.data.frame(data[,1:2],directed=FALSE )
    E(g)$weight = data[,3]
    E(g)$color = "lightgrey"
    # layout
    set.seed(34)   ## to make this reproducable
    l=layout.fruchterman.reingold(g)
    # size
    nodeSize = graph.strength(g)
    V(g)$size = (nodeSize - min(nodeSize))/(max(nodeSize) - min(nodeSize))*20
    centrality = betweenness(g)
    # colors
    require(colorspace)
    pal = function(col, border = "light gray", ...){
      n = length(col)
      plot(0, 0, type="n", xlim = c(0, 1), ylim = c(0, 1),
           axes = FALSE, xlab = "", ylab = "", ...)
      rect(0:(n-1)/n, 0, 1:n/n, 1, col = col, border = border)
    }
    
    colors = heat.colors(37); pal(colors)
    position = rank(-centrality, ties.method = "first")
    V(g)$color = colors[position] 
    # width
    E(g)$width = (log(E(g)$weight)- 8)*1.5# (E(g)$weight-min(E(g)$weight))/(max(E(g)$weight)-min(E(g)$weight))*20
    # label
    nodeLabel = V(g)$name
    V(g)$label.cex = log(centrality+1)/20 + 0.5
    V(g)$label.color = "black"
    # community detection
    fc = fastgreedy.community(g); sizes(fc)
    mfc = membership(fc)
    # for (i in 1:max(mfc)) cat("\n", i, names(mfc[mfc==i]), "\n")
    Q = round(modularity(fc), 3)
    # plot
    drawFigure = function(g){
      plot(g, vertex.label= nodeLabel,  
           edge.curved = FALSE, vertex.frame.color="#FFFFFF",
           layout=l,mark.groups = by(seq_along(mfc), mfc, invisible) )
    }
                  
    drawFigure(g) 
    
    # save png
    png("./all_color2.png",
        width=10, height=10, 
        units="in", res=700)
    drawFigure(g) 
    dev.off()


![](http://chengjun.qiniudn.com/all_color.png)


还可以根据月份来可视化

看一下2006年一月的情况吧：

![](http://chengjun.qiniudn.com/month_color_%201.png)

使用R生成24个月的图片，使用[gifmaker](http://gifmaker.me/)生成GIF动态图片：

