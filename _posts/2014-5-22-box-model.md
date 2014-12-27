---
layout: post
title: CSS 盒模型
category: css
---
## Box module

元素形成了一个矩形的区域，这个区域就是 CSS 中最基本的布局要素， 常被称作 "box"

每个box都包含一个内容区域、内边距区域、边框区域、外边距区域。

![boxmodel](/images/box-model.png)


### margin

**有些情况下，margin不起作用：**

* 对于行内非替换元素（例如 SPAN）垂直方向的margin不起作用

* table 类型中 的 TD TR TH 等margin是不起作用的。


注：替换元素是指 input 、 img等，元素中没有实际内容，浏览器根据元素的标签和属性来决定元素的具体显示内容，也就是说会把元素属性替换成相应的内容。

#### Collapsing margins

##### 什么时候会发生叠加

普通流中相邻的两个块元素在垂直方向上设置的margin会发生叠加。

##### 常见情况

**1.父元素的margin与块级子元素的margin叠加**

父元素没有加border和padding并且父子元素之间没有非空内容时，父元素的margin-top和它的第一个**块级子元素**的margin-top,父元素的margin-bottom和它的最后一个块级子元素的margin-bottom发生叠加。

第一个/最后一个子元素是行内元素则不会发生重叠，且只有父元素的margin值是有效的。


即使父元素并没有设置margin值，但是父子间满足叠加条件时，也会发生叠加，此时的表现就是：给子元素设置垂直margin值没有效果，父元素没有设置垂直margin值，但是在其兄弟元素间应用了子元素的margin值


	div{width:400px; height:100px; background:#505050;}
    
    p{background:yellow;height:50px;margin:20px;}

![collapsing margins](/images/collapsing-margin.png)

   
        
给P设置了上外边距，却没有效果。没有给P的父元素DIV2设置外边距，却与DIV1产生了外边距离，这是因为DIV2与其块级子元素P发生了外边距叠加，所以叠加后DIV2的上外边距为20px。

**2.上下元素的margin叠加**

两个元素都在普通流中，没有float、absolute、inline-block。上一个元素的margin-bottom和下一个元素的margin-top叠加。

**3.元素自身的margin值叠加**

一个没有创建BFC、没有子元素高度为0的元素的margin-top和margin-bottom叠加。

##### 如何避免

* 父子关系中可通过给父元素添加border或者padding

* 兄弟元素中可以通过浮动或者绝对定位其中一个元素

* 能用padding的地方，尽量用padding代替margin

### negative margin

html:

	<div class="img">
		<img src="bio-photo.jpg" alt="">
	</div>
    
css:

	.img{
		background:url(shadow.gif) no-repeat bottom right;
		float:left;
		clear:right;
		margin:100px;
		border:1px solid red;
	}
	.img img{
		display:block;/*解决img标签底部3px留白问题*/
		border:1px solid #a9a9a9;
		padding:4px;
		margin:-20px 5px 5px -20px;
        position:relative;/*解决IE6中默认隐藏负margin部分问题*/
	}
    
![ie-negative-margin](/images/ie-negative-margin.png)

IE6下默认隐藏负margin部分的效果
    
![negative-margin](/images/negative-margin.png)

**父元素的宽高自适应，父元素的宽高不包含子元素的负margin值部分，负margin值部分溢出父元素。**


### width

#### 未声明宽度

盒子总宽 = 左右margin+左右padding+width+左右边框

**1.静态或相对定位的盒子**

盒子未声明宽度，盒子的总宽会继承父元素的宽度，即盒子的总宽保持100%，给盒子加padding和border会减小width值保持盒子总宽不变，所以不会导致溢出

**2.绝对定位或浮动的盒子**

盒子未声明宽度，宽度会自适应内容，直到盒子的总宽度达到父元素的100%，然后折行。

绝对定位或浮动的盒子，宽度自适应内容表现为行内元素的特性，但并没有彻底变为行内元素，因为他们仍然可以设置宽高属性，行内元素是没有宽高属性的。

### background

盒子背景 = 盒子总宽 - margin

盒子的背景是包含盒子的内容、padding和border的。但是border的显示优先权大于背景，所以边框总是显示在背景之上的。


	div{
    	width:350px;
        height:100px;
        background:#a5a5a5;
        border:5px dashed red;
        padding:10px;
    } 

![box-background](/images/box-background.png)


















