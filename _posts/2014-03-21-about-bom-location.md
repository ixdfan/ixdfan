---
layout: post
title: BOM之location对象
---
提供与当前窗口中加载的文档有关的信息，还提供一些导航功能。

它既是window对象的属性，也是document对象的属性。即window.location 和document.location引用的是同一个对象。

它将URL解析为独立的片段，可以通过不同的属性来访问这些片段。

## location对象的所有属性

| 属性名 | 例子 |说明|
|--------|-----|---|
|hash|"#contents"|返回URL中的hash，如果URL中不包含散列则返回空字符串  |
| host       |"www.wrox.com:80"| 返回服务器名称和端口号    |
|    hostname    |   "www.wrox.com"     |返回不带端口号的服务器名称|
|href|"http://www.wrox.com"|返回当前加载页面的完整URL，location对象的toString()也返回这个值|
|pathname|"/WileyCDA/"|返回URL中的目录或文件名|
|port|"8080"|返回URL中指定的端口号，如果不含端口号则返回空字符串|
|protocol|"http:"|返回页面使用的协议，通常是http:或https:|
|search|"?q=javascript"|返回URL的查询字符串，这个字符串以问号开头|

##查询字符串参数

解析查询字符串，然后返回包含所有参数的一个对象

    function getQueryStringArgs(){
        var qs = (location.search.length > 0 ? location.search.substring(1): " ");//取得查询字符串，并去掉开头的问号

        var args = {};

        var items = qs.split("&");//取得每一项

        var item = null;
        var name = null;
        var value = null;

        for(var i = 0 ;i < items.length; i++){//逐个将每一项添加到args对象中
            item = items[i].split("=");
            name = decodeURIComponent(item[0]);
            value = decodeURIComponent(item[1]);
            args[name] = value;
        }
        return args;
    }

## 位置操作

使用location对象可以通过很多方式来改变浏览器位置

### assign()

	location.assign("http://www.wrox.com");

立即打开新URL并在浏览器的历史记录中生成一条记录。

    window.location = "http://www.wrox.com";
    location.href = "http://www.wrox.com";
    
如果将window.loacation或location.href设置为一个URL值，也会以该值调用assign()方法。

在这些改变浏览器位置的方法中，location.href是最常用的。

### 修改location对象的属性来改变当前加载的页面
假设初始URL为 http://www.wrox.com/WileyCDA/

    //将URL修改为http://www.wrox.com/WileyCDA/#section1
    location.hash = "#section1";

    //将URL修改为http://www.wrox.com/WileyCDA/?q=javascript
    location.search = "?q=javascript";

    //将URL修改为http://www.yahoo.com/WileyCDA/
    location.hostname = "www.yahoo.com";

    //将URL修改为http://www.wrox.com/mydir/
    location.pathname = "mydir";

    //将URL修改为http://www.wrox.com:8080/WileyCDA/
    location.port = 8080;
    
每次修改location的属性（hash除外），页面都会以新URL重新加载。

通过上面任何一种方式修改URL之后，浏览器的历史记录中就会生成一条新纪录，可以通过“后退“按钮导航到前一个页面。要禁用这种行为可以使用replace()方法。

### replace()
只接受一个参数，即要导航到的URL

结果会导致浏览器位置改变，但不会在历史记录中生成新纪录。在调用replace方法后，用户不能返回到前一个页面。

### reload()

重新加载当前显示的页面

如果调用reload时不传参，页面就会以最有效的方式重新加载，也就是说，如果页面自上次请求以来并没有改变过，页面就会从浏览器缓存中重新加载。

    location.reload();//重新加载可能从缓存中加载
    location.reload(true);//从服务器重新加载
    
位于reload调用之后的代码可能不会执行，最好将reload放在代码的最后一行。

