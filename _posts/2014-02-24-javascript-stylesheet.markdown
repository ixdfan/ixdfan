---
layout: post
title: JavaScript 操作样式表
---

页面加载时所有外部的和嵌入式的样式表都根据其在文件中出现的位置，按顺序存储在styleSheets数组中，document.styleSheets[0]是第一个样式表。


    document.styleSheets[0].disabled=false;
    //第一个样式表可见。styleSheets数组中每个元素都有一个disabled属性，用于启用或关闭元素功能。

    document.styleSheets[0].cssRules[1].style.color="purple";
    //W3C中通过cssRules数组访问样式表中的具体规则

    document.styleSheets[1].rules[1].style.color="blue";
    //IE中通过rules数组来访问具体规则



style对象包含一系列与浏览器支持的CSS属性相对应的属性。


    style.fontFamily="arial"//style属性中不包含连字符，第一个单词后面的每个单词首字母大写


###visibility属性


    style.visibility="visible"//显示
    style.visibility="hidden"//隐藏

