---
layout: post
title : split方法和join方法
---

## split

split()方法用于把一个字符串分割成字符串数组

stringObject.split(separator,howmany);

separator 必需，字符串或正则表达式，从该参数指定的地方分割stringObject，返回的字符串不包含separator。如果把空字符串用作separator，那么stringObject中每个字符之间都会被分割

howmany 可选，指定返回数组的最大长度，如果没设置整个字符串都会被分割，不考虑它的长度

    var str="How are you doing today?";
    
    alert(str.split(""));//H,o,w, a,r,e, y,o,u, d,o,i,n,g, t,o,d,a,y,?
    
    alert(str.split(" "));//How,are,you,doing,today?
    
    alert(str.split(" ",3));//How,are,you

    var words = sentence.split(/\s+/);//可以使用正则表达式做参数
    
**注意：split()方法中使用正则表达式，分割时不会替换掉捕获组的内容。**

## join

join()用于把数组中的所有元素放入一个字符串

arrayObject.join(separator);

separator 可选，指定要使用的分隔符，如果省略则使用逗号做分隔符

    var arr = new Array("First","second","third");

    alert(arr.join());//First,second,third

    alert(arr.join(""));//Firstsecondthird

    alert(arr.join("."));//First.second.third





