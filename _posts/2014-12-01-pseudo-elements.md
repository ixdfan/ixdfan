---
layout: post
title: 伪元素与伪类
category: CSS
---
## 伪类

伪类主要用于向某些选择器添加特殊效果

### 锚伪类

`:link`和`visited`为链接伪类，只能应用于锚链接。`:hover`、`:active`、`:focus`为动态伪类，可以应用于任何元素

链接的不同状态可以不同的方式显示，这些状态包括：活动状态，已被访问状态，未被访问状态，鼠标悬停状态

	a:link{color:#ff0000}
    a:visited{color:#00ff00}
    a:hover{color:#ff00ff}
    a:active{color:#0000ff}

锚伪类需要按照上面的顺序定义，否则因为层叠的原因会没有效果

### :first-child伪类

	div p:first-child{}/*选择div第一个子元素的p元素*/

### 伪类与CSS类

伪类可以与CSS类配合使用

	a.message:hover{color:#ff0000}
    
伪类也可以与伪类连接在一起使用

	a:visited:hover{color:red}
    
### 伪类兼容性

IE6下完全忽略`:focus`,`:hover`和`:active`伪类只能用于锚链接

IE7任何元素上都支持`:hover`伪类，忽略`:active`和`:focus`伪类

## 伪元素

### 伪类与伪元素的区别

伪类针对特殊状态的元素，伪元素是针对元素中的特定内容

利用伪元素选取元素内容第一个字母、第一行，选取某些内容的前面或后面。伪元素控制的内容实际上和元素是一样的，但是它本身只是基于元素的抽象，并不存在于文档中，所以叫伪元素

### :first-letter和:first-line

* :first-letter 给文本的首字母设置样式

* :first-line  给文本的首行设置样式

这两个伪元素只能用于块级元素

### :before和:after

* :before 在元素的内容前面插入新内容

* :after 在元素的内容后面插入新内容

默认的插入伪元素为行内元素

### 伪元素与CSS类

伪元素可以与CSS类配合使用

	p.article:first-letter{color:#ff0000}
    
### 利用伪元素清除浮动

	.content:after{display:table;content:'';clear:both;}
    .content{zoom:1}/*兼容IE*/




