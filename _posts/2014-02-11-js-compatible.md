---
layout: post
title: JS中常见兼容问题
category: js
---
##  一、 childNodes

### 差异
	
Firefox会将包括空白、换行等文本信息也当做childNodes中的一员。

IE8及其以下版本只将DOM节点当做是childNodes中的一员。

在FF中访问某个元素节点的兄弟节点时出问题，因为它可能根本不是元素节点。

### 解决访问元素节点的相邻节点问题

    function getNextNode(node){
        node = typeof node == "string" ? document.getElementById(node) :node;
        var nextNode = node.nextSibling;
        if(!nextNode){
            return null;
        }
        while(true){
            if(nextNode.nodeType != 1){
                nextNode = nextNode.nextSibling;
            }else{
                break;
            }        
         }
        return nextNode;
    }
    
## 透明度

### 差异

IE下透明是通过滤镜实现的

FF下透明是通过CSS的opacity属性实现的

### 解决透明度的方案

function setOpacity(node,level){
	node = typeof node == "string"?document.getElementById(node) : node;
    if(document.all){
    	node.style.filter ='alpha(opacity = '+level+')';
    }else{
    	node.style.opacity = level;
    }
}

//IE10的解析方式跟FF是相同的，所以这个方法IE10没效果，

## event 对象

### 差异

IE下，event对象时作为window的属性作用于全局作用域的

FF下，event对象是作为事件的参数存在的

### 解决方案

用一个变量指向event对象，然后通过这个变量来访问event对象。

    btn.onclick = function(e){
        e = window.event || e;
    }
    
### event 对象下某些属性的差异

#### 目标元素的差异

IE 通过srcElement属性来访问事件的目标元素

FF 通过target属性来访问

## 取消冒泡

### 差异

IE中，取消冒泡是通过设置event对象的cancelable属性为true来实现的

FF中，通过调用event对象的stopPropagation方法实现的

### 解决方案

    function stopPropagation(e){
        e = window.event || e;
        if(document.all){
            e.cancelBubble = true;
        }else{
            e.stopPropagation();
        }
    }

## 绑定事件

### 差异

IE支持attachEvent()和detachEvent()

FF支持addEventListener()和removeEventListener()

### 解决方案

    function addEvent(node,eventType,handler){
    	node = typeof node =="string"?document.getElementById(node):node;
        if(node.addEventListener){
            node.addEventListener(eventType,handler,false);}else if(node.attachEvent){
            node.attachEvent("on"+eventType,handler);
            }else{
            node["on"+eventType]=handler;
            }
    }
