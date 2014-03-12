---
layout: post
title: CSS-DOM
---

##style属性

文档的每个元素节点都有一个style属性

加号和减号之类的操作符是保留字符	，不允许用在函数或变量的名字里。要引用一个中间带减号的CSS属性时，DOM要求用驼峰命名法。

style属性只能返回内嵌样式 

####何时该用DOM设置样式

**1）根据元素在节点树里的位置来设置样式**

CSS还无法根据元素之间的相对位置找出某个特定的元素，但这对DOM来说却不是什么难题。

    function getNextElement(node){//node是当前元素的下一个元素 
    if(node.nodeType==1){
    return node;
    }
    if(node.nextSibling){
    return getNextElement(node.nextSibling);
    }
    return null;
    }//当前元素的下一个节点元素

**2）根据某种条件反复设置某种样式**

JS特别擅长处理重复性任务，用while或for循环

让表格的行交替改变背景颜色

**3)响应事件**

根据某个元素的行为去改变它的呈现效果，需要决定用CSS来解决还是用DOM来设置样式，需考虑以下因素：

这个问题最简单的解决方案是什么

那种解决方案会得到更多浏览器的支持