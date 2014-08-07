---
layout: post
title: "使用Python自动复制和重命名文本"
date: 2014-08-07 14:14
comments: true
categories: 
- blog
tags:
- 自动复制
---


我喜欢在网页端更新github上的日志，通过设置只显示categories为blog的文档，我可以每次修改一点东西就完全在网页端写日志。图片附件什么的可以放在七牛网站，感觉非常好。

下面是我用来复制和重命名1000个md文本的python代码：


		# -*- coding: utf-8 -*-
		"""
		Created on Thu Aug 07 14:05:09 2014

		@author: chengjun
		"""

		import shutil
		path = "D:/github/chengjun.github.io/_posts/"   

		demo = path + "2010-01-01-demo.md"

		for i in range(1000):
			newFile = path + "2010-01-" + str(i) + ".md"
			print newFile
			shutil.copy(demo, newFile)


![](http://chengjun.qiniudn.com/7.jpg)
