---
layout: post
title: CSS-DOM
category: js
---

##style属性

文档的每个元素节点都有一个style属性

加号和减号之类的操作符是保留字符，不允许用在函数或变量的名字里。要引用一个中间带减号的CSS属性时，DOM要求用驼峰命名法。

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

## gerComputedStyle()

接收两个参数：要取得计算样式的元素、一个伪元素字符串（如“:after”），如果不需要伪元素信息，第二个参数可以是null

返回一个CSSStyleDeclaration对象，其中包含当前元素的所有计算的样式。

	var computedStyle = document.defalutViewgetComputedStyle(elem,null);
    
    alert(computedStyle.width);

IE不支持，IE中每个元素都有一个currentStyle熟悉，这个熟悉是CSSStyleDeclaration的实例，包含当前元素全部计算后的样式。

	var computedStyle = elem.currentStyle;
    
    alert(computedStyle.width);
    
    alert(computedStyle.border);


对于border这样的综合属性，不同的浏览器解释综合属性的方式不同，所以有的浏览器不会返回计算后的border属性的值，但是可以返回细化后的边框相关的属性（如：borderLeftWidth ）。

**所有计算的样式都是只读的，不能修改计算后样式对象中的CSS属性。**

## CSS 规则

CSSStyleRule对象一些常用属性：

* cssText 返回整条规则对应的文本，IE不支持

* selectorText 返回当前规则的选择符文本

* style 一个CSSStyleDeclaration对象，可以通过它设置和取得规则中特定的样式值

### 获取和修改规则

    .box{
        background-color:red;
        width:100px;
        height:200px;
    }
    
    var sheet = document.styleSheets[0];//取得样式表
    
    var rules = sheet.cssRules || sheet.rules;//取得规则列表
    
    var rule = rules[0];//取得第一条规则
    
    alert(rule.selectorText);//.box
    
    alert(rule.style.cssText);//完整的CSS代码
    
    alert(rule.style.backgroundColor);//red

	alert(rule.style.width);//100px
    
    rule.style.width = "200px";//修改样式

### 添加新规则

#### insertRule()

接收两个参数： 规则文本、表示在哪里插入规则的索引

	sheet.insertRule("body{background-color:silver;}",0);

#### addRule() 	

IE的插入规则方法

接收三个参数：选择符文本、CSS样式信息、插入规则的位置（可选）

	sheet.addRule("body","background-color:silver",0);

#### 跨浏览器插入规则

    function insertRules(sheet,selectorText,cssText,position){
        if(sheet.insertRule){
            sheet.insertRule(selectorText+"{"+cssText+"}",position);
        }else if(sheet.addRule){
            sheet.addRule(selectorText,cssText,position);
        }
    }

	insertRule(document.styleSheets[0],"body","background-color:red",0);
    
    
如果添加的规则非常多，这种方法会变得非常繁琐，所以可以采用动态加载样式表的方法。


### 删除规则

#### deleteRule()

接收一个参数：要删除的规则的位置

	sheet.deleteRule(0);

#### removeRule()

IE支持的方法

	sheet.removeRule(0);

#### 跨浏览器删除规则
    
    function deleteRules(sheet,position){
        if(sheet.deleteRule{
            sheet.deleteRule(position);
        }else if(sheet.removeRule){
            sheet.removeRule(position);
        }
    }

	deleteRules(document.styleSheets[0],0);

## 动态加载样式表

	//<link rel="stylesheet" type="text/css" href="styles.css">要动态加载这个外链样式文件

	function loadStyles(url){
    	var link = document.createElement("link");
        link.rel = "stylesheet";
        link.type = "text/css";
        link.href = url;
        var head = document.getElementsByTagName("head")[0];
        head.appendChild(link);
    }	
    
    loadStyles("styles.css");

加载外部样式文件与JS代码的执行没有固定的次序，动态加载外部样式文件是异步的。

动态加载内嵌样式表

    function loadStyleString(css){
        var style = document.createElement("style");
        style.type = "text/css";
        try{
            style.appendChild(document.createTextNode(css));
        }catch(ex){
            style.styleSheet.cssText = css;
        }
        
        var head = document.getElementsByTagName("head")[0];
        head.appendChild(style);
    }
    
    loadstyleString("body{background-color:red}");













