---
layout: post
title: vertical-align
category: css
---

该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。

## 可能的值

* 长度(cm) 通过距离升高或降低元素

* 百分值(%) 相对于line-height值的百分大小升高或降低元素

* baseline/top/middle/bottom 元素的基线/顶端/中垂线/低端与父元素的基线/顶端/中垂线/低端对齐

* sub/super 降低/升高元素的基线到父元素合适的下标/上标位置

* text-top/text-bottom 元素的顶端/低端与父元素内容区域的顶端/低端对齐

当vertical-align的值是百分值时，是相对于此标签继承的line-height值决定的。

IE6/IE7下的vertical-align的百分比值不支持小数line-height。

## 作用

vertical-align 属性设置元素的垂直对齐方式。

定义行内元素的基线相对于该元素所在行的基线的垂直对齐。在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式。