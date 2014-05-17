---
author: admin
comments: true
date: 2013-11-21 07:04:58+00:00
layout: post
category: js
title: 兼容所有浏览器的当前窗口尺寸

---

 以下是兼容所有浏览器的，获取当前窗口尺寸的方法：



    
    <script type="text/javascript">// <![CDATA[
      var width=window.innerWidth;//window.必须要加，因为ie不支持inner，不写会报错
      var height=window.innerHeight;//支持inner的就用这两条语句
      if(typeof width!='number')//兼容ie
      {
       if(document.compatMode=='CSS1Compat')//兼容ie6
       {
         width=document.documentElement.clientWidth;
         height=document.documentElement.clientHeight;//为标准模式的用这个
       }else{
         width=document.body.clientWidth;
         height=document.body.clientHeight;//不是标准模式的用这个
       }
      }
      alert(width);
      alert(height);
    </script>


IE不支持inner方法，要用document方法，但是document方法的性能不如inner方法，所以支持的用inner方法IE用document方法。

IE6在标准模式和非标准模式下的document方法也不一样，所以要先判断模式，再用相应的document方法。
