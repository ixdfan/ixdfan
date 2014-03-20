---
layout: post
title: 事件之内存和性能
tags: 
- 事件
- 内存
- 性能
categories:
-
---
在JS中，添加到页面的事件处理程序数量直接关系到页面的整体运行性能。导致这一问题的原因是多方面的。

首先，每个函数都是对象都会占用内存，内存中的对象越多性能就越差。其次，必须事先指定所有事件处理程序而导致DOM的访问次数，会延迟整个页面的交互就绪时间。

## 事件委托

对事件处理程序过多问题的解决方案就是事件委托。

事件委托利用了事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。

    <ul id="myLinks">
        <li id="goSomewhere">Go somewhere</li>
        <li id="doSomething">Do something</li>
        <li id="sayHi">Say hi</li>
    </ul>

其中包含三个被单击后会执行操作的列表项。按照传统的做法，需要像下面这样为它们添加三个事件处理程序：

    var item1 = document.getElementById("goSomewhere");
    var item2 = document.getElementById("doSomething");
    var item3 = document.getElementById("sayHi");

    item1.onclick = function(){
        location.href="http://www.wrox.com";
    };

    item2.onclick = function(){
        document.title = "I change the document't title";
    };

    item3.onclick = function(){
    alert("hi");	
    }
    
如果在一个复杂的WEB程序中，对所有可单击的元素都采用这种方式，那就会有数不清的代码用于添加事件处理程序。使用事件委托，只需在DOM树中尽量最高的层次上添加一个事件处理程序。

    var list = document.getElementById("myLinks");

    list.onclick = function(event){
        event = EventUtil.getEvent(event);
        var target = EventUtil.getTarget(event);

        switch(target.id){
            case "doSomething":
                document.title = "I changed the document't title";
                break;
            case "goSomewhere":
                location.href = "http://www.wrox.com";
                break;
            case "sayHi":
                alert("sayHi");
                break;
        }
    };


在这段代码里，使用事件委托只为< ul>元素添加一个onclick事件处理程序。由于所有列表项都是这个元素的子节点，而且它们的事件会冒泡，所以单击事件最终会被这个函数处理。事件目标是被单击的列表项，故而可以通过检测ID属性来决定采取适当的操作。

这段代码的事前消耗更低，因为只取得了一个DOM元素，只添加了一个事件处理程序。占用的内存更少。所有用到按钮的事件，都适合采用事件委托技术。

**事件委托与传统的做法相比具有的优点如下：**

* document对象很快就可以访问，而且可以在页面生命周期的任何时点上为它添加事件处理程序，无需等待load事件。只要可点击的元素呈现在页面上，就可以立即准备适当的功能。

* 在页面中设置事件处理程序所需的时间更少。只添加一个事件处理程序所需的DOM引用更少，所花的时间也更少。

* 整个页面占用的内存空间更少，能提升整体性能。

最适合采用事件委托技术的事件包括：click、mousedown、mouseup、keydown、keyup、keypress。虽然mouseover和mouseout事件也冒泡，但要适当处理它们并不容易，而且经常需要计算元素的位置。

##移除事件处理程序

每当事件处理程序指定给元素时，运行中的浏览器代码与支持页面交互的JS代码之间建立一个连接。这种连接越多页面执行起来就越慢。可以使用事件委托限制建立的连接数量，在不需要的时候移除事件处理程序也是解决这个问题的一个方案。

内存中留有那些过时不用的空事件处理程序，也是造成WEB应用程序内存和性能问题的主要原因。

###从文档中移除带有事件处理程序的元素

如果带有事件处理程序的元素被innerHTML删除了，那么原来添加到元素中的事件处理程序极有可能不能被当做垃圾回收。

    <div id="myDiv">
        <input type="button" value="Click me" id="myBtn"/>
    </div>

    <script>
        var btn = document.getElementById("myBtn");
        var myDiv = document.getElementById("myDiv");
        btn.onclick = function(){
            myDiv.innerHTML = "I change it";
        };
    </script>

为避免双击，单击这个按钮时就将按钮移除并替换为一条消息，这是网站设计中非常流行的一种做法。在< div>元素上设置innerHTML可以把按钮移走，但事件处理程序任然与按钮保持着引用关系。有的浏览器再这种情况下不会做出恰当的处理，它们很有可能会将对元素和对事件处理程序的引用都保存在内存中。

最好手工移除事件处理程序

    btn.onclick = function(){
        btn.onclick = null;//移除事件处理程序
        myDiv.innerHTMl = "I change it";
    };

采用事件委托也有助于解决这个问题，如果事先知道将来有可能使用innerHTML替换掉页面中的某一部分，那么就可以不直接把事件处理程序添加到该部分的元素中，而通过把事件处理程序指定给较高层次的元素，同样能处理该区域中的事件。

###卸载页面时

如果在页面被卸载之前没有清理干净事件处理程序，那它们就会滞留在内存中。每次加载完页面再卸载页面时，内存中滞留的对象数目就会增加，因为事件处理程序占用的内存并没有被释放。

最好的做法就是：在页面卸载之前，先通过onunload事件处理程序移除所有事件处理程序。