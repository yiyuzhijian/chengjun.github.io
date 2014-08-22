---
layout: post
title: "使用Python分析社交网络数据"
date: 2014-07-31 17:41
comments: true
categories: 
- 学术
tags:
- python
- 社会网络
---



![](http://graph-tool.skewed.de/static/doc/_images/polblogs_pr.png)

在线社交网站（Online social network sites, OSNSs)为人们提供了一个构建社会关系网络和互动的平台。每一个人和组织都可以通过社交网站互动、获取信息并发出自己的声音，因而吸引了众多的使用者。作为一个复杂的社会系统，在线社交网站真实地记录了社会网络的增长以及人类传播行为演化。通过抓取并分析在线社交网站的数据，研究者可以迅速地把握人类社交网络行为背后所隐藏的规律、机制乃至一般性的法则。

然而在线社交网络数据的获取方法有别于线下社会数据的获取（如普查、社会调查、实验、内容分析等）、数据的规模往往非常大（称之为“大数据”并不为过）、跨越的时间范围也相对较长（与社会调查中的横截面数据相比），常规的数据分析方法并不完全适用。例如传统的社会调查的数据往往样本量有限，而在线社交网络中的样本量可以达到千万甚至更多。因而，研究者迫切得需要寻找新的数据获取、预处理和分析的方法。本章的内容具体包括数据的抓取、数据预处理、数据分析和数据可视化部分。

###Python简介
本章将简要介绍使用python分析社交网络数据的方法。Python是一种广泛使用的高级编程语言，具有可读性强、编写容易、类库丰富等特点。作为一种“胶水语言”，它可以将使用其他语言编写的各种模块（尤其是C/C++）轻松地联结在一起。自从1991年推出第一个正式版本，因其使用方便，Python社区迅速发展，越来越多的程序员开始使用Python编写程序并贡献了各种功能强大的类库。它被TIOBE编程语言排行榜评为“2010年度编程语言”。

除了免费、功能强大、使用者众多之外，与R和MATLAB相比，Python是一门更易学、更严谨的程序设计语言。如同其它编程语言一样，Python语言的基础知识包括：类型、列表（list）和元组（tuple）、字典（dictionary）、条件、循环、异常处理等。关于这些，初阶读者可以阅读《Beginning Python》一书（Hetland, 2005)。作为一个相对非常完善的编程语言，使用Python编写的脚本更易于理解和维护。

另外，Python中包含了丰富的类库。众多开源的科学计算软件包都提供了Python的调用接口，例如著名的计算机视觉库OpenCV。Python本身的科学计算类库发展也十分完善，例如NumPy、SciPy和matplotlib等。就社会网络分析而言，igraph, networkx, graph-tool, Snap.py等类库提供了丰富的网络分析工具。

读者可以根据个人电脑的操作系统安装[相应的Python版本](https://www.python.org/download/)。目前最新的Python版本为3.0，但是通常使用者会选择使用更稳定的2.7版本。虽然使用者也可以使用文本编辑器编写代码，但是使用体验不如使用好的编译器。编译器是编写程序的重要工具。目前，免费的Python编译器有Spyder、PyCharm(免费社区版)、Ipython、Vim、 Emacs、 Eclipse(加上PyDev插件)。对于使用Windows操作系统的用户，推荐使用Winpython。Winpython内置了Spyder为编译器，与Python(x,y)相比大小适中；免安装，下载后解压即可用；安装类库很方便，并且内置了NumPy、SciPy等类库。

###数据抓取
目前社交网站的公开数据很多，为研究者检验自己的理论模型提供了很多便利。例如[斯坦福的社会网络分析项目](http://snap.stanford.edu/data/index.html)就分享了很多相关的数据集。社交网站为了自身的发展，往往也通过各种合作项目（例如腾讯的“犀牛鸟项目”）和竞赛（例如Facebook通过Kaggle竞赛公布部分数据）向研究者分享数据。

但是，有时候研究者还是被迫需要自己收集数据。受限于网站本身对于信息的保护和研究者自身的编程水平，互联网数据的抓取过程依然存在众多问题（比如抽样问题）。

####直接抓取数据
通常的数据抓取遵循可见即可得的规律，即可以观察到的，就可以被抓取。对于网页内容的抓取，可以是把整个网页都存下来，回头再清洗。这样做比较简单有效，但是还是回避不了之后的从html文件中进行的数据提取工作。在下面的例子当中，我们将尝试抓取百度新闻页面（[http://news.baidu.com/](http://news.baidu.com/)）的热点新闻。在这个例子当中，我们要使用urllib2这个类库来获取该网页的html文本。

在获取html之后，我们将使用一个流行的类库BeautifulSoup来解析html并提取我们需要的信息。现在的BeautifulSoup已经发展到第四个版本。可以使用easy_install或者pip install的方法安装。如果读者使用的是Spyder的话，可以点击Tools--Open command prompt。然后，在打开的命令窗口中输入：easy_install beautifulsoup4 就可以了。使用beautifulsoup解析中文html的时候遇到的主要问题多是由encoding造成的。需要使用sys设定默认的encoding方式为gbk，并在BeautifulSoup函数中指定from_encoding为gbk。


	import urllib2
	from bs4 import BeautifulSoup
	import sys
	
	reload(sys)
	sys.setdefaultencoding('gbk')
	
	url = 'http://news.baidu.com/'
	content = urllib2.urlopen(url).read()
	soup = BeautifulSoup(content, from_encoding = 'gbk')
	hotNews = soup.find_all('div', {'class', 'hotnews'})[0].find_all('li')
	for i in hotNews:
	    print i.a.text
	    print i.a['href']

这样就可以抓取当天的热点新闻，输出的结果如下：
		
	习近平：改革惟其艰难 才更显勇毅
	http://china.cankaoxiaoxi.com/2014/0808/454139.shtml
	治疗费政府全担
	http://gb.cri.cn/42071/2014/08/06/2165s4643613.htm
	李克强点赞人物盘点：有女县长也有棒棒军
	http://news.youth.cn/jsxw/201408/t20140808_5605703.htm
	李克强指示地震救灾
	http://yn.yunnan.cn/html/2014-08/07/content_3316250.htm
	云南地震致615人遇难
	http://news.baidu.com/z/ynlddz/new/zhuanti.html
	临时安置点1顶帐篷内住20人
	http://news.youth.cn/gn/201408/t20140808_5607225.htm

####模拟浏览器抓取数据
越来越多的网站要求必须登录才能看到内容，这个时候就需要使用编程软件模拟浏览器登录。登录成功后，就可以抓取内容了。这里举一个抓取聊天论坛帖子列表的例子。这个网站的网络链接为：http://members.lovingfromadistance.com/forum.php， 我们首先写一个叫screen_login的函数。其核心是定义个浏览器对象br = mechanize.Browser()。这个时候，需要借用浏览器的cookie功能，主要借助于cookielib包。代码如下所示：
		
	import mechanize
	import cookielib
	
	def screen_login(): 
	    br = mechanize.Browser()
	    cj = cookielib.LWPCookieJar()
	    br.set_cookiejar(cj)
	    # setting
	    br.set_handle_equiv(True)
	    br.set_handle_redirect(True)
	    br.set_handle_referer(True)
	    br.set_handle_robots(False)
	    # br.set_debug_http(True)
	    # User-Agent (this is cheating, ok?) 
	    br.addheaders = [('User-agent', 'Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.0.1) Gecko/2008071615 Chrome/17.0.963.56 Fedora/3.0.1-1.fc9 Firefox/3.0.1')]
	    br.set_handle_refresh(mechanize._http.HTTPRefreshProcessor(), max_time=1)
	    # Open the login page
	    br.open('http://members.lovingfromadistance.com/login.php?do=login') 
	    br.select_form(nr = 0) # Find the login form
	    br['vb_login_username'] = '你的用户名' 
	    br['vb_login_password'] = '你的注册密码'
	    br.submit() # Submit the form
	    return(br)
	
	br = screen_login()
	
为了从HTML文档提取cookies，首先使用cookielib模块的LWPCookieJar()函数创建一个cookie jar的实例。LWPCookieJar()函数将返回一个对象，该对象可以从硬盘加载Cookie，同时还能向硬盘存放Cookie。之后，通过 br.set_cookiejar(cj)将这个cookie jar关联到mechanize的浏览器对象br上。简单设置一些浏览器属性后，需要定义使用的user-agent。用户代理（User Agent）指的是代表使用者行为的软件，主要是设置浏览器的头文件。

最后是关键的一步，打开登录页面，输入用户名和用户密码。需要使用br.select_form(nr = 0)来找到登录表格。这里nr的设置比较灵活，不同网站的数值不同。然后输入用户名和密码。比如：br['vb_login_username'] = 'Your registered User name'， 这里的vb_login_username也会随着网站本身使用的具体内容而不同。运行br = screen_login()就可以模拟登录成功，然后就可以开始数据抓取和使用BeautifulSoup来进行信息提取的工作了，此处不再赘述。

####基于API接口抓取数据
好在随着数字化媒体浪潮的到来，第三方开发的网站应用已经成为社交网络必不可少的一部分。社交网站为了自身的发展，往往选择向外界开放部分资源，以方便第三方发展基于该社交网站的产品，进而更好吸引使用者使用。比如新浪微博上有着各种不同的APP，这些应用的数据接口（API）就是由新浪微博所提供的。

数据抓取的第一步，就是建立数据连接的工作，以获取社交网站开放数据流的许可。


	#!/usr/bin/env python
	# -*- coding: utf8 -*-
	
	from weibo import APIClient
	import urllib2
	import urllib
	import sys
	import time
	from time import clock
	import csv
	import random
	
	reload(sys)
	sys.setdefaultencoding('utf-8')
	
	'''Step 0 Login with OAuth2.0'''
	if __name__ == "__main__":
		APP_KEY = '663...' # app key
		APP_SECRET = '2fc....' # app secret
		CALLBACK_URL = 'https://api.weibo.com/oauth2/default.html' 
		AUTH_URL = 'https://api.weibo.com/oauth2/authorize'
		USERID = 'w...4' # your weibo user id
		PASSWD = 'w....' #your pw
	
		client = APIClient(app_key=APP_KEY, app_secret=APP_SECRET, redirect_uri=CALLBACK_URL)
		referer_url = client.get_authorize_url()
		print "referer url is : %s" % referer_url
	
		cookies = urllib2.HTTPCookieProcessor()
		opener = urllib2.build_opener(cookies)
		urllib2.install_opener(opener)
	
		postdata = {"client_id": APP_KEY,
					"redirect_uri": CALLBACK_URL,
					"userId": USERID,
					"passwd": PASSWD,
					"isLoginSina": "0",
					"action": "submit",
					"response_type": "code",
					}
		headers = {"User-Agent": "Mozilla/5.0 (Windows NT 6.1; rv:11.0) Gecko/20100101 Firefox/11.0",
					"Host": "api.weibo.com",
					"Referer": referer_url
				}
	
		req  = urllib2.Request(
		   url = AUTH_URL,
		   data = urllib.urlencode(postdata),
		   headers = headers
		   )
		try:
			resp = urllib2.urlopen(req)
			print "callback url is : %s" % resp.geturl()
			code = resp.geturl()[-32:]
			print "code is : %s" %  code
		except Exception, e:
			print e
	
	r = client.request_access_token(code)
	access_token1 = r.access_token # The token return by sina
	expires_in = r.expires_in
	
	print "access_token=" ,access_token1
	print "expires_in=" ,expires_in   # access_token lifetime by second. 
	
	"""save the access token"""
	client.set_access_token(access_token1, expires_in)
	


当然，这首先需要注册和认证。以新浪微博为例，研究者可到其应用开发页面注册 。现在流行的方式是使用OAuth获取连接社会化媒体的API的使用权限。

通过查阅社交网站的API文档，选取适当的API接口，就可以很方便地从社交网站抓取数据了。因为直接从网站数据库获取数据，因而数据结构化较好。获取数据使用许可之后，其使用就非常方便灵活了。




###数据预处理

###数据分析
- 

###可视化

###参考文献
Hetland, Magnus Lie. (2005) Beginning Python: From Novice to Professional. Apress.

Russell, M. A. (2013). Mining the Social Web: Data Mining Facebook, Twitter, LinkedIn, Google+, GitHub, and More. O'Reilly Media, Inc.

Russell, M. A., & Russell, M. (2011). 21 Recipes for Mining Twitter. O'Reilly Media, Inc.

