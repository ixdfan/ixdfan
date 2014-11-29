---
layout: post
title: background详解
category: CSS
---

## background

background是多个背景属性的简写方式，常用背景属性：

* background-color 设置背景颜色

* background-position 设置背景图像的位置

* background-size 设置背景图像的尺寸(CSS3)

* background-repeat 设置如何重复背景图像

* background-origin 设置背景图像的定位区域(CSS3)

* background-clip 设置背景图像的绘制区域(CSS3)

* background-attachment 规定背景图像是否固定或随页面滚动

* background-image 设置要使用的背景图像

background简写顺序：

	background: #fff url(img/test.jpg) no-repeat fixed left top;
    
## background-position

background-position属性设置背景图像的起始位置，可能的值有关键字、百分比、长度，不同类型的值对背景图像的放置有所不同。

### 关键字

用关键字指定背景图像位置时，元素和图像的指定位置重合

	background-position:left top;/* 背景图像的左上角和元素的左上角重合 */
    
    
位置关键字一个对应水平方向，一个对应垂直方向，可以按任何顺序设置。

如果只设置一个关键字，则另一个关键字是center

### 长度值

用长度值指定背景图像起始位置时，图像的左上角和元素的指定位置重合

元素的左上角为（0,0），右下角为（width，height）

	background-position:20px 40px;/* 元素(20px,40px)的点与图像的左上角重合 */
    
###百分比值

用百分比值指定背景图像起始位置时，图像的百分比点和元素的百分比点重合

	background-position:10% 10%;/* 图像(10%,10%)的点和元素(10%,10%)的点重合 */
    
百分比值的定位方式与关键字类似

图像和元素的左上角为（0,0）,右下角为(100%,100%)

### 应用

1.实现CSS Sprite

利用background-position属性，可以指定显示背景图片的某一部分，因此可以将多个图片合成一张图片，选择显示其中某一个部分

	background-position:0 -30px;/* 元素的(0,-30px)点与图像左上角重合，因此从背景图像(0,30px)的点开始显示图像的一部分 */
    
2.流动布局中实现两列等高效果

利用background-position属性，指定背景图像根据浏览器宽度按比例显示图像中的一部分

两列布局的HTML：

	<div class="wrap">
    	<div class="content">content</div>
        <div class="side">side</div>
    </div>
    
CSS：

	.wrap{background:url(img/test.jpg) repeat-y 70% 0}/*图像(70%,0)的点和wrap元素(70%,0)的点重合*/
	.content{width:70%}
    .side{width:30%}

test.jpg是一副2000px*10px的背景图，图的右边30%是side的背景。通过将background-position的值设成百分比值，背景图就能根据wrap的宽度按比例显示side的背景图，以此来显示流动的两列布局

## background-attachment

可能的值：

* scroll 默认值，背景图像会随着页面的滚动而移动

* fixed 当页面的其余部分滚动时，背景图像不会滚动（类似于定位中的固定定位position:fixed）