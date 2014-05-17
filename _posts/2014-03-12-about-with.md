---
layout: post
title: with 语句
category: js
---

with语句的作用是将代码的作用域设置到一个特定的对象中

with(expression) statement

定义with语句的主要目的是简化多次编写同一个对象

    var qs=location.search.substring(1);
    var hostName=location.hostname;
    var url=location.href;
    使用with语句改写
    with(location){//用with语句关联了location对象
    var qs=search.substring(1);
    var hostName=hostname;
    var url=href;
    }
    
在with语句内部，每个变量首先被认为是局部变量，而如果在局部环境中找不到该变量的定义，就会查询location对象中是否有同名的属性，如果发现了同名的属性，则以location对象属性的值作为变量的值。

**大量使用with语句会导致性能下降，同时也会给调试代码造成困难，因此在开发大型应用程序时，不建议使用with语句。**