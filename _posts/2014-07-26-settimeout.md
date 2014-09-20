---
layout: post
category: js
title: 间歇调用和超时调用
---
JavaScript是单线程语言，但它允许通过设置超时值和间歇值来调度代码在特定的时刻执行

### setTimeout()

接收两个参数：要执行的代码、以毫秒表示的时间

第一个参数可以是一个包含JS代码的字符串，也可以是一个函数

    setTimeout("alert('Hello world')",1000);

    setTimeout(function(){alert("Hello world!");},1000);

由于传递字符串可能导致性能损失，因此不建议以字符串作为第一个参数。

为了控制要执行的代码，有一个js任务队列。这些任务会按照他们添加到队列的顺序执行。setTimeout的第二个参数告诉JS再过多长时间把当前任务添加到队列中，如果队列是空的，那么添加的代码会立即执行，如果不是，要等到前面的代码执行完了以后再执行

调用setTimeout()之后，该方法会返回一个数值ID，表示超时调用，这个ID是计划执行代码的唯一标识符，可以通过它取消超时调用。

要取消尚未执行的超时调用计划，可以调用clearTimeout()方法并将相应的超时调用ID作为参数传递给他。

    var timeoutId = setTimeout(function(){alert("Hello world");},1000);

    clearTimeout(timeoutId);//取消

超时调用的代码都是在全局作用域中执行的，因此函数中的this通常指向window对象。

### setInterval()

与超时调用类似，只不过他会按照指定的时间间隔重复执行代码，直至间歇调用被取消或页面被卸载。

接收的参数和setTimeout相同，也会返回相应的ID，可以通过clearInterval(ID)来取消。

最好用超时调用来模拟间歇调用，因为后一个间歇调用可能会在前一个间歇调用结束之前启动。
