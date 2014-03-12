---
layout: post
title: < script> 标记那些事儿
modified: 2014-03-12
category: articles
tags: [something about script]
comments: true
share: true
---


##标签位置
1. ####< script>放在< head>中

    **优点：**把所有外部文件的引用都放在相同的地方

    **缺点：**影响页面加载速度。

    < script> 放在< head>中，就必须等到全部的JS文件被下载、解析和执行完成后，才开始呈现页面内容（浏览器在遇到body标签时才开始呈现页面内容）。这对那些需要很多JS代码的页面来说，会导致浏览器在呈现页面时出现明显的延迟，而且延迟期间浏览器窗口是一片空白。
    
2. ####< script>放在< /body>前

	**优点：**解析JS之前，页面已经完全呈现在浏览器中。页面内容加载更快，用户体验更好。

## 嵌入 or 外部文件

#### 使用< script>嵌入JS代码

不要在代码的任何出现"< /script>"字符串

    <script>
    function sayScript(){

           alert("</script>");
    }
    </script>	

浏览器加载这段代码时会出错，因为按解析嵌入式代码的规则，当遇到"< /script>"字符串时，就会认为那是结束标签。

正确的表达方式：alert("</scr"+"ipt>");
    
    
#### 使用< script>引入外部JS文件

用于引入外部文件的< script>标签中间不应该再包含额外的JS代码

    <script src="wrap.js"></script>  
    <script src="wrap.js">alert("wrong");</script>这种写法是错误的。  
    <script>标签的src属性可以包含来自外部域的文件  
    <script src="http://www.somewhere.com/afile.js"></script>

标签中的src属性指向当前HTML页面所在域之外的某个域中的url

**注意：**在访问自己不能控制的服务器上的JS文件时要多加小心，随时可能遇到别人恶意的修改代码。

==< script>引入外部文件的优点:==

**可维护性**——开发人员可在不触及HTML标签的情况下，集中精力编辑JS代码

**可缓存**——浏览器可根据具体的设置缓存所有的外部JS文件。如果有两个页面都使用同一个文件，那这个文件只需下载一次，这样能加快页面加载速度。

## 浏览器不支持

< body>< noscript>能出现在文档中的任何HTML元素（< script>除外）都可以放在这里< /noscript>< /body>

浏览器不支持脚本，或脚本被禁用时，<noscript>中的内容才会显示
