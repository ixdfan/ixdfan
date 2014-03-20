---
author: admin
comments: true
date: 2014-02-06 11:44:59+00:00
layout: post

title: 构造函数与类

---

构造函数是一种特殊的函数，通常首字母大写。函数名当做对象的类名称，函数体定义其属性和方法。

类是一个模板。汽车类定义了汽车的属性和方法，然后我们用这个类做模板可以创建任意多个汽车对象。JS中没有class类关键字，要创建一个JS类，即编写一个构造函数。



    
    	
    function Book(title,author){
        this.title=title;
        this.author=author;
        this.show=function(){alert(this.title);};//定义一个方法,this指向当前对象（book）
    }
    var book=new Book("js","smith");//new 关键字调用构造函数，创建一个book实例
