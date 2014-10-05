---
layout: post
title: CSS默认样式
category: css
---
### 标签的默认样式

为保证没有样式表的页面能够正常显示，浏览器在加载一个页面的时候会判断这个页面是不是存在对应的CSS样式表，如果没有，就加载浏览器默认的CSS样式表，以保证页面信息能够被正常读取。

#### 1.body标签

* 有默认的margin值

* display:block;

#### 2.a标签

* 有默认的字体颜色，即color属性有默认值，各浏览器有所不同。

* text-decoration:undeline; 链接文字默认带下划线

* a:visited{ color:#800080;} 访问后的链接文字带有默认颜色

#### 3.h类标签

* font-size 有默认的字体大小，各级标题默认大小不一样

* font-weight:bold; 默认加粗
 
* margin 有默认的上下外边距，各浏览器有所不同

#### 4.ul和ol

* margin 有默认的margin值，各个浏览器不同

* padding 有默认的padding值

* list-style-position:outside

* list-style-type  ul的默认值是disc ol的默认值是decimal

#### 5.dl、p、form

* margin 有默认的margin值

#### 6.input

* border-style:inset 有默认的边框样式

* border-width 有默认的边框宽带

* font-family 有默认的字体

* font-size 有默认的字体大小

* overflow:hidden 默认的溢出隐藏

* padding 默认的内边距

#### 7.button

* background-color 有默认的背景颜色

* border-style 有默认的边框样式

* border-width 有默认的边框宽度

* font-family 有默认的字体

* font-size 有默认的字体大小

* overflow 有默认的溢出隐藏

* text-align:center 有默认的文字居中

* box-sizing:border-size 部分浏览器有默认的盒子解析方式，即宽度包含了边框和内边距

* padding 部分浏览器有默认内边距

#### 8.fieldset

* border-style:groove 有默认的边框样式

* border-width:2px; 有默认的边框宽度

* padding 部分浏览器有默认的内边距

* margin 部分浏览器有默认的外边距

#### 9.legeng

* padding 部分浏览器有默认的内边距

#### 10.optgroup和option

* font-family:sans-serif 有默认的字体

* font-size:10pt 有默认的字体大小

* font-style:italic 有默认的字体形状

* font-weight:bold 默认加粗

#### 11.select

* border-color 

* border-style

* border-width:2px

* font-family

* font-size

* overflow:hidden

* box-sizing:border-box

#### 12.textarea

* border-style:inset

* border-width:2px

* font-family

* font-size

* overflow-x:hidden

* overflow-y:scroll

* padding

* white-space:pre

#### 13.table

* border-color

* border-spacing 部分浏览器（IE8+）

* box-sizing:border-box IE8+

#### 14.tbody、thead

* border-color

* display: tbody是table-row-group，thead是table-header-group IE8+

* display:block IE7-

* vertical-align:middle

#### 15.tfoot、tr

* border-color IE7-

* display:tfoot是table-row-group，tr是table-row IE8+

* vertical-align:middleIE8+

#### 16.td、th

* border-color

* padding

* display:table-cell IE8+

* vertical-align:middle Ie8+

* text-align:center  th的默认属性

* font-weight:bold th的默认属性

有时候给父元素设置某个属性，发现子元素没有变化，可能就是子元素已经有默认的此属性了

### 默认有外边距的标记

body,dd,dl,fieldset,form,h,hr,menu,ol,p,ul

### 默认有内边距的标记

button,caption,fieldset,input,legend,menu,ol,td,texterea,th,ul

