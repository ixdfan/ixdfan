---
layout: post
title: BOM之history对象
category: js
---
history对象保存着用户上网的历史记录，从窗口被打开的那一刻算起。

因为history是window对象的属性，因此每个浏览器窗口、每个标签页、每个框架都有自己的history对象与特定的window对象关联。

## go()
使用go()方法可以在用户的历史记录中任意跳转，可以向前也可以向后。

接收一个参数：表示向后或向前跳转的页面数。负数表示向后

给go()传递一个字符串参数时，浏览器会跳转到历史记录中包含该字符的第一个位置，如果历史记录中不包含该字符串则什么也不做。

    history.go(1);//前进一页
    history.go(-1);//后退一页
    history.go("wrox.com");//跳转到包含wrox.com的最近的一页

back()和forword()来代替go(),这两个方法模仿浏览器的前进和后退。

    history.back();
    history.forword();
    
## length

history的length属性保存着历史记录的数量

对于加载到窗口、标签页和框架中的第一个页面而言，history.length等于0，通过检测该属性的值，可以确定用户是否一开始就打开了这个页面

    if(history.length == 0){

    }