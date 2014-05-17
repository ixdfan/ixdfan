---
layout: post
title: 事件之事件对象
category: js
---
在触发DOM上的某个事件时，会产生一个事件对象event，这个对象中包含着所有与事件有关的信息。包括导致事件的元素、事件的类型以及其他与特定事件相关的信息。

例如，鼠标操作导致的事件对象中，会包含鼠标位置的信息；键盘操作导致的事件对象中，会包含与按下键有关的信息。

## DOM中的事件对象

兼容DOM的浏览器会将一个event对象传入到事件处理程序中。无论指定事件处理程序时使用什么方法（DOM0级或DOM2级），都会传入event对象。

    var btn = document.getElementById("myBtn");

    btn.onclick = function(event){
        alert(event.type);
    }

    btn.addEventListener("click",function(event){
    alert(event.type);
    },false);
    
这两个事件处理程序都会弹出一个警告框，显示由event.type属性表示的事件类型

**event对象包含与创建它的特定事件有关的属性和方法**

所有事件都会有下表列出的成员

* bubbles  表明事件是否冒泡

* cancelable	 是否可以取消事件的默认行为

* currentTarget  事件处理程序正在处理事件的那个元素（注册事件的元素）

* detail   与事件相关的细节信息

* eventPhrase  调用事件处理程序的阶段：1表示捕获阶段，2表示目标阶段，3表示冒泡阶段

* preventDefault() 取消事件的默认行为，如果cancelable是true，则可以使用这个方法

* stopPropagation()  取消事件的进一步或冒泡。如果bubbles是true则可以使用这个方法

* target  事件的目标

* type 被触发的事件类型

* view 与事件关联的抽象视图，等同于发生事件的window对象

### this == currentTarget    

在事件处理程序内部，对象**this**始终等于**currentTarget**的值，而**target**则只包含事件的实际的目标

    var btn = document.getElementById("myBtn");
    document.body.onclick = function(){
        alert(event.currentTarget);//document.body
        alert(event.target);//btn
    }
    
当单击按钮时，this和currentTarget都等于document.body，因为事件处理程序是注册到这个元素上的，而target等于按钮元素，因为它是click事件真正的目标。由于按钮上并没有注册事件处理程序，结果click事件就冒泡到document.body,在那里事件才得到了处理。

### 处理多个事件

**在需要通过一个函数处理多个事件时，可以使用type属性**

    var btn = document.getElmentById("myBtn");

    var handler = function (event){
        switch(event.type){
            case "click":
                alert("Clicked");
                break;
            case "mouseover":
                alert("Mouseover");
                break;
            case "mouseout":
                alert("Mouseout");
                break;
        }
    };

    btn.onclick = handler;
    btn.onmouseover = handler;
    btn.onmouseout = handler;

###阻止默认行为

preventDefault()阻止事件的默认行为。例如，链接的默认行为就是在被单击时会导航到其href属性指定的URL，如果想阻止链接的这一默认行为，那么通过链接的onclick事件处理程序就可以取消它。

    var link = document.getElementById("myLink");
    link.onclick = function(event){
        event.preventDefault();
    };

只有cancelable属性值为true的事件，才可以使用preventDefault来取消其默认行为。

### 取消冒泡

stopPropagation()用于立即停止事件在DOM层次中传播，取消进一步事件捕获或冒泡

    var btn = document.getElmentById("myBtn");
    btn.onclick = function(){
        alert("Clicked");
        event.stopPropagation();
    };

    document.body.onclick = function(){
        alert("Body Clicked");
    };

stopPropagation()阻止事件传播到document.body，因此不会触发注册在此元素上的事件处理程序。

### eventPhase

    var btn = document.getElementById("myBtn");

    btn.onclick = function(event){
        alert("Clicked");
        alert(event.eventPhase);// 2 事件处理程序处于目标对象上
    };

    document.body.addEventListener("click",function(event){
        alert(event.eventPhase);//1 捕获阶段调用的事件处理程序
    },true);

    document.body.onclick = function(event){
        alert(event.eventPhase);//3 冒泡阶段调用的事件处理程序
    };

单击按钮时， 首先执行的是在捕获阶段添加到document.body中的那一个事件，然后会触发按钮上注册的事件，最后触发在冒泡阶段添加到document.body上的事件。

只有在事件处理程序执行期间，event对象才会存在，一旦事件处理程序执行完后，event对象就会被销毁。

##IE中的事件对象

在使用DOM0级方法添加事件时，event对象作为window对象的一个属性存在。

使用attachEvent添加事件，event对象作为参数被传入事件处理程序中。

通过HTML属性添加事件，通过一个名叫event的变量来访问event对象。

    var btn = document.getElementById("myBtn");

    btn.onclick = function(){
        var event = window.event;
        alert(event.type);
    }

    btn.attachEvent("onclick",function(event){
        alert(event.type);//click
    });

    <input type="button" value="Click me" onclick="alert(event.type);">

**IE中事件对象包含下表所列的属性和方法**

* cancelBubble  默认值为false，将其设置为true可以取消事件冒泡

* returnValue	默认值为true，将其设置为false就可以取消默认行为

* srcElement	事件的目标

* type	被触发的事件的类型

IE中事件处理程序的作用域根据指定它的方式来确定，所以不能认为this等于事件目标，最好还是用srcElement来确定。

###returnValue和cancelBubble

    var link = document.getElementById("myLink");

    link.onclick = function(){
        window.event.returnValue = false;//阻止默认行为
        window.event.cancelBubble = true;//取消冒泡
    };

    document.body.onclick = function(){
        alert("Body clicked");
    };

##跨浏览器事件对象

    var EventUtil = {
        getEvent: function(event){
             return event ？ event:window.event;
        },

        getTarget: function(event){
            return event.target||event.srcElement;
        },

        preventDefault: function(event){
            if(preventDefault){
                event.preventDefault();
            }else{
                event.returnValue = false;
            }
        },

        stopPropagation: function(event){
            if(stopProgation){
                event.stopProgation();
            }else{
                event.cancelBubble = true;
            }
        }
    };

    var btn = document.getElementById("myBtn");
    btn.onclick = function(event){
        event = EventUtil.getEvent(event);//获取event对象
        var target = EventUtil.getTarget(event);//获取目标元素
        EventUtil.preventDefault(event);//取消默认行为
        EventUtil.stopPropagation(event);//取消冒泡
    };