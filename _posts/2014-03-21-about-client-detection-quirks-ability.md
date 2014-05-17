---
layout: post
title: 客户端检测之怪癖检测
category: js
---
##能力检测

不到万不得已就不要使用客户端检测，只要能找到更通用的方法，就使用更通用的方法。先设计最通用的方案，再使用特定于浏览器的技术增强该方案。

能力检测的目标不是识别特定的浏览器，而是识别浏览器的能力。

### 能力检测的要点
* 先检测达成目的的最常用的特性。以保证代码最优化，因为多数情况下都可以避免测试多个条件。

* 必须测试实际要用到的特性。一个特性存在并不意味着另一个特性也存在。

如果知道自己的应用程序需要使用哪些特定的浏览器特性，最好一次性检测所有相关特性，而不要分别检测。

    //确定浏览器是否支持Netscape风格的插件
    var hasNSPlugins = !!(navigator.plugins && navigaror.plugins.length);

    //确定浏览器是否具有DOM1级规定的能力
    var hasDOM1 = !!(document.getElementById && document.getElementsByTagName && document.createElement);

在实际的开发中，应该将能力检测作为确定下一步解决方案的依据，而不是用它来判断用户使用的是什么浏览器。

##怪癖检测

怪癖检测的目标是识别浏览器的特殊行为，指定浏览器存在什么缺陷。

例如，IE中存在一个bug,如果某个实例属性与标记为[[DonEnum]]的某个原型属性同名，那么该实例属性就不会出现在for-in循环中。

**检测这种怪癖**

    var hasDontEnumQirck = function(){
        var o = {toString:function(){}};
        var count = 0;
        for(var prop in o){
            if(prop == "toString"){
                count++;
            }
        }return (count>1);
    }();
    
如果浏览器存在这个bug，那么使用for-in循环枚举带有自定义的toString方法的对象，就会返回两个toString的实例。

由于检测怪癖涉及运行代码，因此最好只检测那些有直接影响的怪癖，而且最好在脚本一开始就执行此类检测，以便尽早解决问题。

