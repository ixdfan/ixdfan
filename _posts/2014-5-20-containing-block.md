---
layout: post
title: containing block
category: css
---
## Containing block

### 为什么要理解包含块

宽度高度自动值的计算、浮动元素定位、绝对定位元素的定位等都跟包含块有关。

### 怎么找一个元素的包含块

![包含块判定](/images/Containblock.png)


#### 静态或相对定位元素的包含块

position值为static或relative的元素，它的包含块由它最近的块级、单元格或者行内块祖先元素的**内容框**创建。

#### 绝对定位元素的包含块

绝对定位元素的包含块由离他最近的position属性为absolute、relative或者fixed的祖先元素创建。

如果其祖先元素是行内元素，则包含块取决于其祖先元素的"direction"属性

如果 'direction' 是 'ltr'，包含块的顶、左边是祖先元素生成的第一个框的顶、左内边距边界(padding edges) ，右、下边是祖先元素生成的最后一个框的右、下内边距边界(padding edges) 

![绝对定位元素的包含块](/images/CBabsolute.png)

行内元素内形成的包含块，在各浏览器中各不相同，存在兼容性问题。

**如果祖先元素不是行内元素，那么包含块的区域是祖先元素的内边距边界**
