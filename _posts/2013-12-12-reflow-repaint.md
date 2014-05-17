---
layout: post
title: reflow
category: font-end
---
## 页面渲染过程


* 解析HTML代码并生成一个 DOM 树。 

* 解析CSS文件，顺序为：浏览器默认样式->自定义样式->页面内的样式。 生成一个渲染树（render tree），这个渲染树和DOM树的不同之处在于，它是受样式影响的。它不包括那些不可见的节点


 

## reflow

浏览器为了重新渲染部分或全部的文档而重新计算文档中元素的位置和几何结构的过程。

### 什么时候会引起回流

* 调整窗口大小

* 改变字体

* 增加或者移除样式表

* 内容变化，比如用户在input框中输入文字

* 激活 CSS 伪类，比如 :hover 

* 操作 class 属性

* 脚本操作 DOM

* 计算 offsetWidth 和 offsetHeight 属性

* 设置 style 属性的值 


### 减小回流

* 减少不必要的DOM深度。改变DOM节点树上任何一个层级都会影响节点树的每个层级——从根结点一直到修改的子节点。不必要的节点深度将导致执行回流时花费更多的时间。

* 避免设置多项内联样式,因为每个都会造成回流，样式应该合并在一个外部类，这样当该元素的class属性可被操控时仅会产生一个reflow。

* 如果你想让复杂的表现发生改变，例如动画效果，在这个流动线之外实现它。使用position-absolute或position-fixed来实现它。

* 应用元素的动画，使用 position 属性的 fixed 值或 absolute 值,它们不影响其他元素的布局，他们只会导致重新绘制，而不是一个完整回流。这样消耗会更低。

* 避免使用CSS的JavaScript表达式



## repaint

当一个元素的外观发生改变的时候，重绘(repaint)也随之发生，但是不影响布局。例如：outline, visibility, or background color



