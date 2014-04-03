---
layout: post
title: hasLayout和BFC
---
## hasLayout

haslayout 是IE渲染引擎的一个内部组成部分。

渲染引擎采用hasLayout 的属性，属性值可以为true或false。当一个元素的 hasLayout 属性值为true时，这个元素有一个布局（layout）

当一个元素有一个布局时，它负责对自己和可能的子孙元素进行尺寸计算和定位。
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

