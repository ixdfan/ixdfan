---
layout: post
title: Document 对象
---

## document对象的属性

### document.title

document.title 包含着< title >元素中的文本，通过这个属性可以取得当前页面的标题，修改title属性的值不会修改< title >元素

### document.URL

document.URL 包含页面完整的URL

### document.domain

document.domain 包含页面的域名

URL和domain属性是相互关联的，domain可以设置，但是不能设置为URL中不包含的域

如果URL中包含一个子域名“p2p.wrox.com”,那么只能将domain设置为“wrox.com”

如果页面中包含来自其他子域的框架或内嵌框架，由于跨域安全限制，来自不同子域的页面无法通过JS通信，而通过将每个页面的document.domain设置为相同的值，这些页面就可以互相访问对方的JS对象了。

例如：有一个页面加载自www.wrox.com，其中包含一个内嵌框架，框架内的页面加载自p2p.wrox.com，将这两个页面的domain值都设置为wrox.com，他们之间就可以通信了。

如果域名一开始是松散的，就不能再设置为紧绷的。如：document.domain设置为wrox.com后就不能再设置为p2p.wrox.com，否则会导致错误。

### document.referrer

document.referrer 保存着链接到当前页面的那个页面的URL

在没有来源页面的情况下，referrer属性中可能包含着空字符串

## 查找元素方法

### document.getElmentById()

通过元素ID获取元素

### document.getElementsTagName()

IE将注释实现为元素，在IE中调用document.getElementsByTagName("*")返回的节点中包含注释节点

### document.getElementsByName()

HTMLDocument类型才有这个方法

### document.getElementsByClass()

## 文档写入

### write()与writeIn()

接收一个参数，即要写入到输出流中的文本

write()会原样写入，writeIn()会在字符串末尾添加一个换行符

字符串中包含HTML标签，会创建一个DOM元素而且可以在将来访问该元素。

    document.write("< strong >加粗< / strong>");//加粗
    
可以使用write()动态包含外部资源

	document.write("< script src="file.js">"+"</scri"+"pt>");//不能直接包含< /script >

在页面加载中调用document.write()，直接向其中输出内容

如果再页面加载结束后再调用document.write()，那么输出的内容将会重写整个页面。

    window.onload = function(){
        document.write("Hello world");//页面上别的内容都没有了，只有hello world
    }


### open()与close()

分别用于打开和关闭网页的输出流，如果在网页加载期间使用write()则不需要用到这两个方法。

































