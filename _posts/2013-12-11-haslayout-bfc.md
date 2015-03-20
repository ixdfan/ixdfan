---
layout: post
title: hasLayout和BFC
category: css
---
## hasLayout

IE显示引擎使用一个称为布局的内部概念。布局问题是许多IE显示Bug的根源。

### 什么是布局

IE使用布局概念来控制元素的尺寸和定位，那些拥有布局的元素负责本身及其子元素的尺寸设置和定位。如果一个元素没有拥有布局，那么它的尺寸和位置由最近的拥有布局的祖先元素控制。

IE显示引擎利用布局概念减少它的处理开销。在理想情况下，所有元素都控制自己的尺寸和定位，但是这在IE中会导致很大的性能问题，因此IE开发团队决定只将布局应用于实际需要的元素上，来减少性能开销。

#### 默认有布局的元素

* body
* html
* table
* tr、td
* img
* hr
* input、selsect、textarea、button
* iframe、embed、object、applet

haslayout 是IE渲染引擎的一个内部组成部分。

渲染引擎采用hasLayout 的属性，属性值可以为true或false。当一个元素的 hasLayout 属性值为true时，这个元素有一个布局（layout）

### 与layout可能引发的问题

* IE 很多常见的浮动问题。

* 元素本身对一些基本属性的异常处理问题。

* 容器和其子孙之间的空白边重叠问题。

* 使用列表时遇到的问题。

* 背景图像的定位偏差问题。

* 使用脚本时遇到的浏览器之间处理不一致的问题。


### 怎么激发hasLayout

大部分IE问题，都可以通过激发元素的 haslayout 属性来解决。

**触发方式有以下几种：**

* display: inline-block

* height: 任何值除了auto

* float: left 或 right

* position: absolute

* width: 任何值除了auto

* writing-mode: tb-rl

* zoom: 除 normal 外任意值

**IE7中以下属性也能触发布局:**

* overflow: hidden 、scroll 或auto

* min-width

* max-width 除none之外的任何值

### 布局的影响

#### 1.布局对浮动的影响

如果一个文本段落靠着一个浮动元素，标准浏览器中文本围绕这个元素，IE6中如果段落拥有布局那么它被限制为矩形阻止文本围绕浮动元素。

#### 2.布局影响元素的尺寸

如果元素的内容比元素本身大，我们希望内容溢出到元素外，IE6中拥有布局的元素会错误地扩展以便适应内容的尺寸。

#### 3.	其他问题

* 拥有布局的元素不会收缩

* 布局元素对浮动自动清理

* 相对定位的元素没有布局

* 拥有布局的元素之间外边距不叠加

* 没有布局的块级链接上，单击区域只覆盖文本


## BFC

BFC(Block Formatting Context)，“块级格式化范围“提供了一个独立布局的环境，每个BFC都遵守同一套布局规则。

### BFC的特点

* BFC中的元素的布局是不受外界的影响

* 块元素与行元素都会垂直的沿着其父元素的边框排列

* 盒子从顶端开始垂直地一个接一个地排列，两个盒子之间的垂直的间隙是由他们的margin 值所决定的

* 两个相邻的块级盒子的垂直外边距会产生折叠

* 每一个盒子的左外边缘会触碰到容器的左边缘

* 容器里面的子元素不会在布局上影响到外面的元素

* 创建了BFC的元素不能与浮动元素重叠

### 产生BFC

* float：left|right

* position：absolute|fixed

* display: table-cell|table-caption|inline-block

* overflow: hidden|scroll|auto

