---
layout: post
title: 相对/绝对定位详解
category: css
---
## 绝对定位

* 绝对定位的框从常规流中脱离。对其后的兄弟元素的定位没有影响。

* 绝对定位元素定位的参照物是其包含块，不一定是其父元素。

* 绝对定位框有外边距(margin)， 它们不会和其它任何外边距发生折叠（Collapsing margins）。

* 一般情况下绝对定位和固定定位的元素， 在 3D 的可视化模型中，处于浮动元素的上方。

* 一个绝对定位框会为它的常规流子元素和定位子元素(不包含 fiexed 定位的元素)生成一个新的包含块。 不过，绝对定位元素的内容不会在其它框的周围排列。

常规流中的框，都在同一个层上，浮动框是处于常规流之上的一个特殊层，它可能会对常规流中的框的定位产生影响。但绝对定位的框不会， 每个绝对定位的框都可以看做一个单独的图层，不会对其他层框的定位产生影响。




特性：

* 和浮动定位一样具有包裹性

* 和浮动定位一样具有破坏性

* 少用绝对定位布局

* 绝对定位布局影响扩展和维护，影响流动布局

绝对定位于浮动定位一样具有包裹性和破坏性。

### 包裹性

包裹性，即让元素inline-block化，简单的说就是让元素变成具有宽高属性的行内元素。

例如：设置了宽高的块级元素应用了绝对定位，其宽高就变成自适应内部元素。

float也会让元素inline-block化，对行内元素应用了浮动定位，它就具有了宽高属性。

### 破坏性

浮动定位的破坏性在于切断line box 链，导致高度坍塌。

绝对定位的破坏性在于不占实体位置，导致高度和宽度都坍塌。

### 影响流动布局

流动布局强调不定宽、不定高，由于绝对定位的破坏性会导致高度宽度坍塌，所以需要给父元素设定固定的宽高，否则可能会发生重叠，这样就影响了流动布局。

不要用绝对定位来做普通布局。

### 绝对定位的使用

#### 把绝对定位元素放在合适的位置

绝对定位不是通过relative限制，而是直接相对于body，通过触发元素的偏移值设定位置，把绝对定位的元素放在body标签下，这样更高效。

绝对定位元素被relative限制在很深的DOM节点中，增加了DOM的复杂度，不利于维护；越深的DOM元素，回流越强；增加了CSS代码的消耗量；

#### margin定位替代绝对定位

实现相同的布局效果，margin使用更少的代码而且布局的扩展性更强。

绝对定位布局，父元素的属性改变，可能会导致布局错乱，而margin则不会。

某些情况下，margin值的改变会产生更强的回流，性能上比绝对定位低，例如：用margin和绝对来实现滚动播放。

#### 用绝对定位来实现元素隐藏
	//方式一
    .hidden{
        position:absolute;
        top:-9999em;
    }

	//方式二
    .hidden{
        position:absolute;
        visibility:hidden;
    }

	//方式三
    .hidden{
        position:absolute;
        clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
        clip: rect(1px, 1px, 1px, 1px);
    }
    
    //显示时设置position:static;

绝对定位隐藏元素的特点：

* 绝对定位隐藏元素具有更好的可访问性，使用display:none和visibility:hidden隐藏元素，辅助阅读设备无法识别隐藏的内容。

* 如果隐藏元素含有链接元素或是可获得焦点的控件元素，但是又是使用的可用性隐藏。这些隐藏的链接与控件也是可以响应键盘焦点Tab切换的，这会让键盘使用用户产生不解与疑惑的

* 使用absolute隐藏或显示元素会产生重绘而不会产生强烈的回流。使用display:none不仅会重绘，还会产生回流，DOM影响范围越广，回流越强烈。

#### 绝对定位实现等高布局

利用绝对定位元素无高度无宽度的特性，可以伪造一个高度足够高的绝对定位层（设置背景色，边框等属性），同时设置父标签溢出隐藏，其多出来的高度就不会显示了，也就实现了看上去的等高布局效果。

    <div class="wrap">
        <div class="left">
            <div class="equal"></div>
            <div class="left_con"></div>
        </div>
        <div class="right"></div>
    </div>
    

    .wrap{overflow:hidden;position:relative;background:#ccc;width:100%;}
    .left{float:left;position:relative;width:25%;}

    .equal{width:100%;height:999em;position:absolute;left:0;top:0;border-right:1px solid #000;background:#fff;}
    .left_con{position:relative;}//设置相对定位的作用是，让内容位于绝对定位背景层的上面。
    
    .right{float:right;width:75%;}
    
    
## 相对定位

一个框按照常规流或者浮动得到定位，它还可以相对该位置偏移，这就是相对定位。

* 相对定位的框B不会对后面的框A有影响：后面的框就像B没有发生偏移一样,即B偏移后，A不会重新定位

* 相对定位元素处于常规流中，相对于元素在常规流中的原位置进行定位，偏移后，在常规流中依然占据原位置，这也意味着相对定位可能产生框的重叠。

* 如果相对定位引起"overflow:auto"或"overflow:scroll"框的溢出，会创建需要的滚动条，这可能会影响布局。而且存在兼容性问题。

* 相对定位与绝对定位设置相同的z-index值，后设置在上面显示。

### 相对定位的应用

#### 解决IE6下负margin值带来的bug

元素负margin超出父标签的部分会被隐藏。

通过设置margin负值元素的position属性值为relative来解决这个bug

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

其他浏览器效果

#### 把相对定位元素用在合适的标签上

在需要设置一个相对定位元素来限制绝对定位时，不要把相对定位设置在最外层父标签上，在绝对定位元素外套一层标签专门用于设置相对定位，这样具有更好的可扩展性。

## 常见的几种定位方式

* 元素定位到左上角——用绝对定位+margin值来实现

* 元素定位到右上角——用浮动+相对定位来实现

* 元素定位到右下角——用最近父标签相对定位+元素绝对定位实现

## z-index

z-index 只有在position不是static的情况下才有作用。

如果元素A要在元素B之上显示，那么先设置B的position属性，再设置A的position属性就可以了，不用再设置两者的z-index.

### z-index为负值

将元素的z-index设置为负值，给元素设置监听事件时会出问题。

z-index为负值的元素，位于z-index为0的body之下，被透明的body挡住了，以至于不能触发事件。

### flash

flash插入网页中，如果和其他元素有重叠，无论怎么设置z-index，Flash都浮在其他元素之上。

这是因为浏览器解析页面时，会先判断元素的类型，如果是窗口类型的，会优先于非窗口类型的元素显示在页面最顶端，如果同属非窗口类型的，才会去判断z-index的大小。

flash嵌入网页中，有个`wmode`属性，用于指定窗口模式，其值有：window（窗口）、opaque(非窗口不透明)、transparent(非窗口透明)。默认为wmode的值为window，其Z轴优先级高于所有非窗口类型元素

	<object width="640" height="90" type="application/x-shockwave-Flash">
    	<param name="movie" value="xxx.swf"></param>
        <param name="wmode" value="opaque"></param>
        <embed width="640" height="90" wmode="opaque" type="application/x-shockwave-Flash" src="xxx.swf"></embed>
    </object>


### IE6下select元素

IE6下select元素也是以窗口形式显示的。

IE6下select会浮在定位元素之上,增加一个放在select上面其他元素下面的iframe来解决

HTML：

	<select>
    	<option>请选择</option>
    </select>
    <div class="test"></div>
    <iframe id="mask" frameborder="0" scrolling="no"></iframe>
    
CSS：

	.test{width:200px;height:200px;background:green;position:absolute;left:50px;top:10px;z-index:5;}
    #mask{width:200px;height:200px;position:absolute;left:50px;top:10px;z-index:4;}










