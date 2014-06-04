---
layout: post
title: line-height 那些事儿
category: css
---
## line-height的理解

![行高](/images/o_line_height.png)


* 行内元素和块级元素都具有line-height属性

* 行高=行框的高度=行内最高行内框的高度

* 内容区=顶线和底线间的距离

* 行内元素如em、strong、span等，其padding、margin、border-top、border-bottom 不会增加行高。


## line-height的继承性与优先级

### 继承

#### 可能的值

* %

* em

* px

* 纯数字

line-height的值是可继承的，子元素会继承父元素的line-height的值。

**父元素的line-height设置为百分值、像素值、em值，子元素继承的是计算后的值，设置为纯数字子元素直接继承数字值。**

    <p>
        <span>子元素继承父元素的line-height值</span>
    </p>
    
    p{line-height:xxxx;font-size:12px;}
    span{font-size:20px;}
    
当p元素的行高设置为200%时，span元素的行高继承父元素的24px,当p的行高设置为2时，span元素继承的是2即40px.



### 优先级

在IE6/7中，如果行内子元素与块级父元素设置了不同的line-height值，会以行内子元素设置的值为准，而其他浏览器则以块级父元素设置的值为准。当行内子元素设置为行内块时，IE6会直接忽略块级父元素设置的line-height值。

    <p>
        <span>
        在IE6/7中，如果行内子元素与块级父元素设置了不同的line-height值，会忽略块级父元素的line-height值以行内子元素设置的值为准，而其他浏览器则以块级父元素设置的值为准。
        </span>
        <i>&nbsp;<i>//为了多行居中时兼容IE6
    </p>


    p{line-height:500px;border:1px solid #000;width:300px;}

    span{vertical-align:middle;line-height:100px;}


基于上面的兼容性问题，要让多行文字在固定高度的块级元素中垂直居中显示，需要如下设置：

    p{line-height:500px;border:1px solid #000;width:300px;height:500px;}//height为了兼容IE6

    span{vertical-align:middle;line-height:100px;display:inline-block;}

    i{display:inline-block;vertical-align:middle;font-size:0;}//兼容IE6
    
## line-height 与 height

某些情形下，line-height与height可以互换，因为实现的效果一样都能撑开一个高度。

**差异：** height会使标签haslayout,而line-height则不会。
