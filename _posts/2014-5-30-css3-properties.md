---
layout: post
title: CSS 常用属性
category: css
---

### box-sizing

改变默认盒模型，IE8以下不支持

    box-sizing:content-box;//默认的盒模型，在宽度和高度之外绘制元素的内边距和边框

    box-sizing:border-box;//在已设定的宽度和高度之内绘制内边距和边框
    
需要给元素设定相对大小的宽高，并且设定内边距和边框时，此时不知道该用宽高的相对大小减去几个百分点。这时使用box-sizing就很方便，不用考虑内边距和边框，因为他们会在设定的宽高之内绘制。

	li{
    	width:20%;
        box-sizing:border-box;
        border:10px solid #000;
    }//有5个li元素，20%的宽度正好占满父元素,也不会因为加了border而产生溢出
    
### text-transform

控制文本的大小写

    text-transform:none;//默认值

    text-transform:capitalize;//每个单词以大写字母开头

    text-transform:uppercase;//所有字母都大写

    text-transform:lowercase;//所有字母都小写


### transition

IE10以前不支持，Safari支持-webkit-transition

	transition: property duration timing-function delay;
    
    property设置过渡效果的CSS属性的名称
    
    duration 完成过渡效果需要的时间（秒或毫秒）
    
    timing-funciton 速度效果的速度曲线
    
    delay 过渡开始时间
    
duration一定要设置，否则默认时长为0，就不会产生过渡效果


