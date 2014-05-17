---
author: admin
comments: true
date: 2014-02-06 11:30:28+00:00
layout: post
category: js
title: for/in循环


---

**for/in循环，常用来遍历对象属性或数组元素**
  

1.for/in获取数组元素索引，遍历数组元素

    var p=['a','b','c'];
    
    for(var property in p){
    document.write(p[property]+"</br>");
    }
    
把a ,b ,c的索引一个个赋给property,而不是直接把a , b ,c赋给property


2.for/in获取对象属性名，遍历对象属性

    for(var property in navigator){
    document.write(property+":"+navigator[property]+"</br>");
    }//把navigator对象的属性名一个一个赋给property，而不是直接把属性值赋给property

**navigator[property]**,用数组的方法访问对象的属性。
