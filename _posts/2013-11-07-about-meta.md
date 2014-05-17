---
layout: post
title: meta 元标记
category: html
---
元标记meta提供有关页面的元信息，比如针对搜素引擎和更新频度的描述和关键词。
##keywords

    <meta  name="keywords"  content="用户会搜索的与该网页相关的关键词">

关键词大众化之外要加点与别人不一样的内容，有助于搜索优化。

**关键词的格式与要求：**


1.关键字间用逗号隔开，不要用空格或”|“

2.关键字应该是短语

3.关键字内容要与网页核心内容相关，不要重复使用关键词否则可能被搜索引擎惩罚。

4.最多包含3~5个关键字，每个网页的关键字应该不一样

	<meta  name="description"  content="对关键字的描述">

简略描述网页的关键内容，通常被搜索引擎用于搜索结果页上展示给最终用户的一段文字片断。


##author
	<meta  name="author"  content="作者名">设置作者，写的意义不大

##字符集

	<meta  http-equiv="content-type"  content="text/html;charset=gb2312">

设置字符集（不设置字符集，一般默认为gb2312，文件保存时选择utf8就会出现乱码）


##定时刷新

	<meta  http-equiv ="refresh"  content="跳转时间"  url="http://www.baidu.com">//设置页面定时跳转，跳转到百度。

