---
layout: post
title: 事件之事件处理程序
category: js
---

##事件处理程序

响应某个事件的函数就叫做事件处理程序或事件侦听器。

事件处理程序的名字以"on"开头，例如 onclick

##为事件指定处理程序的方式

###1.HTML事件处理程序

	<input type="button" value="Click me" onclick="showMessage();alert('Clicked');">

通过指定onclick属性，并将JS代码作为它的值来定义。由于这个值是JS，因此不能使用未经转义的HTML语法字符，如 & “” < >

HTML中定义的事件处理程序可以包含要执行的具体动作，也可以调用在页面其他地方定义的脚本

事件处理程序中的代码在执行时，有权访问全局作用域中的任何代码

**在HTML中指定事件处理程序有两个缺点：**

* 存在一个时差问题。用户可能会在HTML元素一出现在页面上就触发相应的时间，但当时的事件处理程序可能还不具备执行条件，例如脚本在元素下方或页面最底部定义的。

* HTML和JS代码紧密耦合。如果要改变事件处理程序要改动两个地方，HTML代码和JS代码

###2.DOM0级事件处理程序

将一个函数赋值给一个事件处理程序属性


    var btn = document.getElementById("myBtn");
    btn.onclick=function(){
        alert("Clicked");

    }
    
简单，所有浏览器都支持

在这些代码运行以前不会指定事件处理程序，因此如果这些代码在页面中位于按钮后面，就有可能在一段时间内怎么单击都没有反应

DOM0级方法指定的事件处理程序被认为是元素的方法，因此这时候的事件处理程序是在元素的作用域中运行，程序中的this引用当前元素

    btn.onclick = function(){
        alert(this.id);
    }

单击按钮弹出的是元素的ID

以这种方式添加的事件处理程序会在事件流的冒泡阶段被处理

删除事件处理程序

btn.onclick = null;

再单击按钮将不会有任何动作发生

###3.DOM2级事件处理程序

**addEventListener()**	、**removeEventListener()** ,他们都接收三个参数：要处理的事件名、作为事件处理程序的函数、一个布尔值。

布尔值如果是true，表示在捕获阶段调用事件处理程序，如果是false表示在冒泡阶段调用事件处理程序。大多数情况下都是将事件处理程序添加到事件流的冒泡阶段，这样可以最大限度的兼容各种浏览器

**DOM2级方法的主要好处是：可以添加多个事件处理程序。**

    btn.addEventListener("click",function(){
    alert(this.id);},false);
    
    btn.addEventListener("click",function(){
    alert("hello world");},false);

这里添加的事件处理程序也是在其依附的元素的作用域中运行的。这两个事件处理程序会按照他们的顺序触发

移除时使用的参数和添加时使用的参数相同，这也意味着通过addEventListener()添加的匿名函数将无法移除

	btn.removeEventListener("click",function(){
    alert(this.id);
    },false);

移除事件时的匿名函数和添加事件时的匿名函数时完全不同的函数

	var handler=function(){
    alert(this.id);
    };
    
    btn.addEventListener("click",handler,false);
    
    btn.removeEventListener("click",handler,false);

这种方式能有效移除事件处理程序，因为参数中使用了相同的函数

### 4.IE事件处理程序

**attachEvent()**、 **detachEvent()** ,这两个方法接收相同的两个参数：事件处理程序名称、事件处理程序函数

IE只支持事件冒泡，所以通过**attachEvent()**添加的事件处理程序都会被添加到冒泡阶段

    btn.attachEvent("onclick",function(){
    alert("Clicked");
    });
    
**IE中使用attachEvent()与使用DOM0级方法的主要区别在于事件处理程序的作用域**

DOM0级方法下，事件处理程序会在其所属的元素的作用域内运行。使用attachEvent，事件处理程序会在全局作用域中运行，因此**this等于window**

**attachEvent()**也可以为一个元素添加多个事件处理程序，不过这些事件处理程序不是以添加他们的顺序执行，而是以相反的顺序被触发。

使用attachEvent添加的事件可以通过detachEvent来移除，条件是提供相同的参数。

### 5.跨浏览器的事件处理程序

要保证处理事件的代码能在大多数浏览器下一致的运行，只须关注冒泡阶段

    var EventUtil = {
        //跨浏览器添加事件
        addEvent: function(element,type,handler){
            if(element.addEventListener){
                element.addEventListener(type,handler,false);  
            }
            else if(element.attachEvent){
                element.attachEvent("on"+type,handler);
            }
            else{
            element["on"+type]=handler;
            }
        }

        //跨浏览器移除事件
        removeEvent: function(element,type,handler){
        if(element.removeEventListener)
            element.removeEventListener(type,handler,false);
        }
        else if(element.detachEvent){
            element.detachEvent("on"+type,handler);
        }
        else{
            element["on"+type] = null;
        }


    }

创建方法addEvent() removeEvent()用于添加和删除事件，这两个方法属于一个名叫EvenUtil的对象，用这个对象来处理浏览器之间的差异

















