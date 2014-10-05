---
layout: post
title: html and body
category: css
---
html元素和body元素都是块级元素

html元素的尺寸由浏览器窗口控制

html元素默认是overflow:auto，所以导致浏览器滚动条出现

overflow:visible默认值，内容不会被修剪，会呈现在元素框之外

hidden 内容会被修剪，并且其余内容是不可见的

scroll不论是否需要，都会出现滚动条内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容

auto溢出时内容被修剪，显示滚动条以便查看其余的内容


body元素默认是position:static 定位的子元素都是相对html元素定位的

![html body](/images/html-body.png)

