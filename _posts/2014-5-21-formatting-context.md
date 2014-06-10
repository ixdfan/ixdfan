---
layout: post
title: Formatting context
category: css
---

## Formatting context

格式化上下文指的是初始化元素定义的环境。

上下文定义了元素所处的环境，格式化表明元素处于此环境中应当被初始化。

### Block formatting context

在块格式化上下文中，框一个接一个的被垂直放置，他们的起点是一个[包含块](http://ixdfan.com/css/2014/05/20/containing-block.html)的顶部。



###触发方式

* 浮动元素

* 绝对定位元素

* 行内块元素

* 单元格
 
* 表格标题元素

* overflow非visible的元素

这些元素会创建新的块格式化上下文

### 特性

* 可以包含浮动元素

* 可以阻止外边距折叠

* 可以阻止元素被浮动元素覆盖

### Inline formatting context

行格式化上下文中，框一个接一个的水平排列，起点是包含块的顶部。

### 行框（line boxes）

![行框](/images/scope_line_box.png)

通常，行框的左右边接触到其包含块的左右边，但是浮动元素可能处于包含块边缘和行框边缘之间。

同一行内格式化上下文中的行框通常高度不一样，如一行包含了高的图形。

![行框](/images/line_box.png)


#### 行内框在行框中的对齐

##### 垂直方向上的对齐

行内框在行框中垂直方向上的对齐取决于vertical-align特性，默认为baseline对齐

![行内框垂直对齐](/images/line_box_align.png)

vertical-align = "top",行内框顶端与行中最高元素的顶外边界对齐。

##### 水平方向上的对齐

行内框宽度总和小于包含他们的行框的宽，他们在水平方向上的对齐，取决于text-align特性。

![行内框水平对齐](/images/inline_box_horizontal_align.png)

text-align="center",行内框在行框中居中对齐

行内框超出包含它的行框的宽度，它会被分割成几个框，并且这些框会被分布到几个行框内

![行内框宽度超过行框](/images/inline_box_break.png)
