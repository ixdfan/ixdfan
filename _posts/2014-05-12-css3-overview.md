---
layout: post
title: CSS3
category: css
---

## CSS3 模块

CSS3 被划分为模块。

其中最重要的 CSS3 模块包括：

* 选择器
* 框模型
* 背景和边框
* 文本效果
* 2D/3D 转换
* 动画
* 多列布局
* 用户界面

## CSS3 边框

通过 CSS3，能够创建圆角边框，向矩形添加阴影，使用图片来绘制边框

三个重要属性：

* border-radius
* box-shadow
* border-image

Internet Explorer 9+ 支持 border-radius 和 box-shadow 属性。

Firefox、Chrome 以及 Safari 支持所有新的边框属性。

对于 border-image，Safari 5 以及更老的版本需要前缀 -webkit-。

Opera 支持 border-radius 和 box-shadow 属性，但是对于 border-image 需要前缀 -o-。

### 圆角
向 div 元素添加圆角：

    div
    {
    border:2px solid;
    border-radius:25px;
    -moz-border-radius:25px; /* Old Firefox */
    }


### CSS3 边框阴影

在 CSS3 中，box-shadow 用于向方框添加阴影：

    div
    {
    box-shadow: inset 10px 10px 5px #888888;
    }

 第1个长度值用来设置对象的阴影水平偏移值。可以为负值

 第2个长度值用来设置对象的阴影垂直偏移值。可以为负值 

 如果提供了第3个长度值则用来设置对象的阴影模糊值。不允许负值
 
 如果提供了第4个长度值则用来设置对象的阴影外延值。不允许负值

 设置对象的阴影的颜色。

inset： 设置对象的阴影类型为内阴影。该值为空时，则对象的阴影类型为外阴影 



### 图片边框
使用图片创建围绕 div 元素的边框：

    div
    {
    border-image:url(border.png) 30 30 round;
    -moz-border-image:url(border.png) 30 30 round; /* 老的 Firefox */
    -webkit-border-image:url(border.png) 30 30 round; /* Safari 和 Chrome */
    -o-border-image:url(border.png) 30 30 round; /* Opera */
    }

如果最后是一个round则表示水平和垂直方向均使用该值，如果是2个round值，则第一个为水平方向属性，第二个为垂直方向属性。round表示平铺，stretch表示拉伸

## 背景

* background-size
* background-origin
* background-clip

background-size 属性规定背景图片的尺寸。以像素或百分比规定尺寸。如果以百分比规定尺寸，那么尺寸相对于父元素的宽度和高度。

background-origin 属性规定背景图片的定位区域。背景图片可以放置于 content-box、padding-box 或 border-box 区域。

background-clip 规定背景的绘制区域 content-box、padding-box 或 border-box 区域。

    background-origin:content-box;
    background-size:100% 100%;
    
#### CSS3 允许为元素使用多个背景图像。

为 body 元素设置两幅背景图片：

    body
    { 
    background-image:url(bg_flower.gif),url(bg_flower_2.gif);
    }

## 文本效果
* text-shadow
* word-wrap

所有主流浏览器都支持 word-wrap 属性。

注释：Internet Explorer 9 以及更早的版本，不支持 text-shadow 属性。

规定水平阴影、垂直阴影、模糊距离，以及阴影的颜色：

向标题添加阴影：

    h1
    {
    text-shadow: 5px 5px 5px #FF0000;
    }

word-wrap 属性允许您允许文本强制文本进行换行 - 即使这意味着会对单词进行拆分：
允许对长单词进行拆分，并换行到下一行：

    p {word-wrap:break-word;}

## 转换
够对元素进行移动、缩放、转动、拉长或拉伸。

转换是使元素改变形状、尺寸和位置的一种效果。

Chrome 和 Safari 需要前缀 -webkit-。

注释：Internet Explorer 9 需要前缀 -ms-。

2D 转换方法：

* translate()——translate(50px,100px) 把元素从左侧移动 50 像素，从顶端移动 100 像素。

* rotate()——元素顺时针旋转给定的角度。允许负值，元素将逆时针旋转。

* scale()—— scale(2,4) 把宽度转换为原始尺寸的 2 倍，把高度转换为原始高度的 4 倍。

* skew()—— skew(30deg,20deg) 围绕 X 轴把元素翻转 30 度，围绕 Y 轴翻转 20 度。

* matrix()——matrix() 方法把所有 2D 转换方法组合在一起。matrix() 方法需要六个参数，包含数学函数，允许：旋转、缩放、移动以及倾斜元素。

3D 转换来对元素进行格式化。

 3D 转换方法：
 
* rotateX()
* rotateY()

Chrome 和 Safari 需要前缀 -webkit-。

Opera 仍然不支持 3D 转换（它只支持 2D 转换）。

通过 rotateX() 方法，元素围绕其 X 轴以给定的度数进行旋转。

通过 rotateY() 方法，元素围绕其 Y 轴以给定的度数进行旋转。


## 过渡
通过 CSS3，我们可以在不使用 Flash 动画或 JavaScript 的情况下，当元素从一种样式变换为另一种样式时为元素添加效果。

Safari 需要前缀 -webkit-。

注释：Internet Explorer 9 以及更早的版本，不支持 transition 属性。

注释：Chrome 25 以及更早的版本，需要前缀 -webkit-。

CSS3 过渡是元素从一种样式逐渐改变为另一种的效果。

要实现这一点，必须规定两项内容：

* 规定您希望把效果添加到哪个 CSS 属性上
* 规定效果的时长

应用于宽度属性的过渡效果，时长为 2 秒：

    div
    {
    transition: width 2s;
    -moz-transition: width 2s;	/* Firefox 4 */
    -webkit-transition: width 2s;	/* Safari 和 Chrome */
    -o-transition: width 2s;	/* Opera */
    }


注释：如果时长未规定，则不会有过渡效果，因为默认值是 0。

效果开始于指定的 CSS 属性改变值时。

如需向多个样式添加过渡效果，请添加多个属性，由逗号隔开：

	transition: width 2s, height 2s, transform 2s;

## 多列
CSS3 多列

通过 CSS3，您能够创建多个列来对文本进行布局 - 就像报纸那样！

在本章中，您将学习如下多列属性：
•column-count——规定元素应该被分隔的列数：
•column-gap——列之间的间隔：
•column-rule——设置列之间的宽度、样式和颜色规则。

Firefox 需要前缀 -moz-。

Chrome 和 Safari 需要前缀 -webkit-。

注释：Internet Explorer 9 以及更早的版本不支持多列属性。



























