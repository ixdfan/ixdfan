---
layout: post
title: BOM之window对象
category: js
---
BOM提供了很多对象，用于访问浏览器的功能，这些内容与任何网页内容无关。

BOM的核心是window对象，他表示浏览器的一个实例。

在浏览器中，window对象既是通过JS访问浏览器窗口的一个接口，又是ECMAScript规定的Global对象。这意味着在网页中定义的任何一个对象、变量和函数都以window作为其Global对象。

## 全局作用域
在全局作用域中声明的所有变量、函数都会变成window对象的属性和方法。

    var age = 29;//在全局作用域中声明的变量是window对象的一个属性
    
    function sayAge(){//在全局作用域中声明的函数是window对象的方法
        alert(this.age);//全局函数中，this=window
    }

    sayAge();//29
    alert(window.age);//29
    window.sayAge();//29
    
## 窗口关系及框架
如果页面中包含框架则每个框架都有自己的window对象，并且保存在frames集合中。
### window对象和top对象
在frames集合中，可以通过数值索引或者框架名称来访问相应的window对象。每个window对象都有一个name属性，其中包含框架的名称。最外层窗口的window对象的name属性不包含任何值，除非这个窗口是通过window.open()打开的。

    <frameset rows="160,*">
        <frame src="frame.html" name="topFrame"/>
        <frameset>
            <frame src="anotherframe.html" name="leftFrame"/>
            <frame src="yetanotherframe.html" name="rightFrame"/>
        </frameset>
    </frameset>
    
在这个框架集中，可以通过window.frames[0]或者window.frames["topFrame"]来引用上方的框架。不过最好通过top.frames[0]或者top.frames["topFrame"]来访问。

top对象始终指向最外层框架，也就是浏览器窗口，使用它可以确保在一个框架中正确访问另一个框架。因为对于在一个框架中编写的任何代码来说，其中的window对象指向的都是那个框架的特定实例，而不是最外层的框架。

也可以直接通过frames[i]或者frames["name"]来访问

### parent对象
parent对象始终指向当前框架的直接上层框架。

在没有框架的情况下，parent和top都等于window对象。

如果代码位于topFrame中，则parent指向的是top

### self
他始终指向window

所有这些对象都是window对象的属性，可以通过window.parent、window.top等形式来访问。

在使用框架的情况下，浏览器中会存在多个Global对象，在每个框架中定义的全局变量会自动成为框架中window对象的属性。由于每个window对象都包含原生类型的构造函数，因此每个框架都有一套自己的构造函数，这些构造函数一一对应，但并不相等。例如：top.Object和top.frames[0].Object并不相等。这个问题会影响到对跨框架传递的对象使用instanceof操作符。


## 窗口位置
### 使用下列代码可以跨浏览器取得窗口左边和上边的位置

    var leftPos = (typeof window.screenLeft == "number") ? window.screenLeft:window.screenX;

    var topPos = (typeof window.screenTop == "number") ? window.screenTop:window.screenY;

在IE、Safari、Opera和Chorme中，支持screenLeft和 screenTop

在Firefox中支持screenX 和screenY

在IE、Opera和Chrome中，screenTop的值需要加上浏览器工具栏的高度。

### 移动窗口
#### moveTo()
接收两个参数，即新位置的x 和 y 坐标

#### moveBy()
接收两个参数，即在水平和垂直方向上移动的像素

    window.moveBy(0,100);//将窗口向下移动100像素
    window.moveTo(200,300);//将窗口移动到(200,300)

这两个方法可能会被浏览器禁用，且不适用于框架，只能对最外层的window对象使用。

## 窗口大小
### 跨浏览器取得页面视口大小

    var pageWidth = window.innerWidth;
    var pageHeight = window.innerHeight;

    if(typeof pageWidth != "number") {
        if(document.compatMode == "CSS1Compat"){//兼容IE6标准模式
            pageWidth = document.documentElement.clientWidth;
            pageHeight = document.documentElement.clientHeight;
        }else{//兼容IE6混杂模式
            pageWidth = document.body.clientWidth;
            pageHeight = document.body.clientHeight;
        }
    }
    
在Safari和Firefox中，outerWidth和outerHeight返回浏览器窗口本身的尺寸。

在Chrome中，innerWidth和outerWidth返回相同的值，即视口的大小而非浏览器窗口的大小。

### 调整浏览器窗口大小
#### resizeTo()
接收两个参数，即浏览器窗口的新宽度和新高度
#### resizeBy()
接收两个参数，即新窗口与窗口的宽度和高度之差。

    window.resizeTo(100,100);//调整到100*100
    window.resizeBy(100,50);//调整到（100+100） * （100+50）
    
这两个方法可能被浏览器禁用，而且不适用于框架，只能对最外层的window对象使用。

## 导航和打开窗口
### window.open()
#### 参数
接收四个参数：要加载的URL、窗口目标、一个特性字符串、表示新页面是否取代浏览器历史记录中当前加载页面的布尔值。

通常只须传递第一个参数，最后一个参数只在不打开新窗口的情况下使用。

如果传递的第二个参数是已有窗口或框架的名称，那么就会在该名称的窗口或框架中加载第一个参数指定的URl。

第二个参数也可以是_self、_parent、 _top、 _blank

    window.open("http://www.wrox.com/","topFrame");
    //如果有一个名叫topFrame的窗口或者框架，就会在该窗口或框架中加载这个URL，否则，就会创建一个新窗口并将其命名为topFrame

#### 弹出窗口
如果第二个参数并不是已存在的窗口或框架，就会根据第三个参数传入的字符串创建一个新窗口或新标签页。如果没有传入第三个参数，就打开一个带有全部默认设置的新浏览器窗口。在不打开新窗口时，会忽略第三个参数。

第三个参数是逗号分隔的设置字符串，表示新窗口都显示哪些特性，可以设置的选项有：

* fullscreen——yes或no——表示浏览器窗口是否最大化，仅限IE

* height——数值——表示新窗口的高度，不能小于100

* left——数值——表示新窗口的坐标，不能是负数

* location——yes或no——是否在浏览器窗口中显示地址栏，不同浏览器的默认值不同

* menubar——yes或no——是否在浏览器窗口中显示菜单栏，默认为no

* resizable——yes或no——是否可以通过拖动浏览器窗口的边框改变其大小，默认为no

* scrollbars——yes或no——如果内容在视口显示不下，是否允许滚动，默认为no

* status——yes或no——是否在浏览器窗口中显示状态栏，默认为no

* toolbar——yes或no——是否在浏览器窗口中显示工具栏，默认为no

* top——数值——新窗口的上坐标，不能是负值

* width——数值——新窗口的宽度，不能小于100


        winodw.open("http://www.wrox.com/","wroxWindow","height=400,width=400,top=10,left=10,resizable=yes");

打开一个新的可以调整大小的窗口，窗口初始大小为400*400，距离屏幕上左各10像素。

window.open()方法会返回一个指向新窗口的引用，我们可以对其进行更多的控制。有些浏览器可能在默认情况下不允许我们针对浏览器窗口调整大小或移动位置，但却运行我们针对通过window.open()创建的窗口调整大小或移动位置。

### window.close()
关闭新打开的窗口

这个方法仅适用于window.open()打开的弹出窗口。

弹出窗口可以在不经用户允许的情况下关闭自己。

弹出窗口关闭之后，窗口的引用还在，除了检测其closed属性外，没有其他用处了。
    window.close();
    alert(window.closed);//true
    
新创建的window对象有一个opener属性，其中保存着打开他的原始窗口对象。这个属性只在弹出窗口的最外层window对象中有定义，而且指向调用window.open()的窗口或框架。但原始窗口中并没有这样的指针指向弹出窗口。

    alert(wroxWin.opener==window);//true
    wroxWin.opener = null;//新创建的标签页不需要与打开他的标签页通信，可以在独立的进程中运行
    
### 弹出窗口屏蔽程序
1.浏览器内置的屏蔽程序阻止的弹出窗口

如果是浏览器内置的屏蔽程序阻止弹出窗口，那么window.open()很可能会返回null，只要检测这个返回值就可以确定弹出窗口是否被屏蔽了。

    var wroxWin = window.open("http://www.wrox.com","_blank");
    if(wroxWin == null){
        alert("The popup was blocked");
    }

2.浏览器扩展或其他程序阻止弹出窗口

如果是浏览器扩展或其他程序阻止弹出窗口，那么window.open()通常会抛出一个错误。因此要想准确的检测出弹出窗口是否被屏蔽，必须在检测值的同时，将对window.open()的调用封装在一个try-catch块中。

    var blocked = false;
    try{
        var wroxWin = window.open("http://www.wrox.com","_blank");
        if(wroxWin == null){
            blocked = true;
        }
    }catch(ex){
        blocked = true;
    }
    if(blocked){
        alert("The popup was blocked");
    }

## 间歇调用和超时调用

JavaScript是单线程语言，但它允许通过设置超时值和间歇值来调度代码在特定的时刻执行

### setTimeout()
接收两个参数：要执行的代码、以毫秒表示的时间

第一个参数可以是一个包含JS代码的字符串，也可以是一个函数

    setTimeout("alert('Hello world')",1000);
    
    setTimeout(function(){alert("Hello world!");},1000);
    
由于传递字符串可能导致性能损失，因此不建议以字符串作为第一个参数。

调用setTimeout()之后，该方法会返回一个数值ID，表示超时调用，这个ID是计划执行代码的唯一标识符，可以通过它取消超时调用。

要取消尚未执行的超时调用计划，可以调用clearTimeout()方法并将相应的超时调用ID作为参数传递给他。

    var timeoutId = setTimeout(function(){alert("Hello world");},1000);

    clearTimeout(timeoutId);//取消
    
超时调用的代码都是在全局作用域中执行的，因此函数中的this通常指向window对象。

### setInterval()
与超时调用类似，只不过他会按照指定的时间间隔重复执行代码，直至间歇调用被取消或页面被卸载。

接收的参数和setTimeout相同，也会返回相应的ID，可以通过clearInterval(ID)来取消。

最好用超时调用来模拟间歇调用，因为后一个间歇调用可能会在前一个间歇调用结束之前启动。

## 系统对话框
显示这些对话框的时候代码会停止执行，而关掉这些对话框后代码又会恢复执行。
### alert()
接收一个字符串并将其显示给用户。
### prompt()
用于提示用户输入一些文本

接收两个参数：要显示给用户的文本提示、文本输入域的默认值

返回文本输入域的值

    var result = prompt("What is your name"," ");
    if(result != null){
        alert("Welcome,"+result);
    }
    
### confirm()

    if(confirm("Are you sure?")){
        alert("I'm so glad you're sure!");
    }else {
        alert("I'm sorry to hear you're not sure.");
    }
    
根据用户选择，返回true或者false

这些系统对话框适合向用户显示信息并请用户做出决定，由于不涉及HTML、CSS或JS，因此他们是增强WEB应用程序的一种便捷方式。

### print()

	window.print();//显示打印对话框
  

### find()

	window.find();//显示查找对话框

print()和 find()都是异步显示的，能将控制权交还给脚本。