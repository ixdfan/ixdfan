---
layout: post
title: BOM之navigator对象
category: js
---
navigator对象的属性通常用于检测显示网页的浏览器类型。

## 检测插件
### plugins
通过plugins数组来检测特定的插件

**plugins数组中的每一项都包含下列属性：**

* name——插件的名字

* description——插件的描述

* filename——插件的文件名

* length——插件所处理的MIME类型数量

#### refresh()
plugins数组有一个refresh()方法，用于刷新plugins以反映最新安装的插件。

接收一个参数：表示是否应该重新加载页面的一个布尔值，如果设置为true则会重新加载包含插件的所有页面；否则只更新plugins数组不重新加载页面。

####检测插件

    function hasPlugin(name){
        name = name.toLowerCase();//将传入的名称转换为小写形式，便于比较
        for(var i = 0; i<navigator.plugins.length;i++){
            if(navigator.plugins[i].name.toLowerCase().indexOf(name) > -1){//比较的字符串都使用小写形式，避免因大小写不一致导致的错误
                return true;
            }
        }return false;
    }
	alert(hasPlugin("Flash")); 
    
hasPlugin函数接收一个参数，要检测的插件名。



### 检测IE中的插件

使用专有的ActiveXObject类型，并尝试创建一个特定插件的实例。IE是以COM对象的方式实现插件的，而COM对象使用唯一标识符来标志。因此，要检测特定的插件，就必须指定其COM标识符。例如，Flash的标识符是ShockwavaFalsh.ShockwaveFalsh

#### 检测IE中是否安装插件

    function hasIEPlugin(name){
        try{//尝试创建一个COM对象的实例
            new ActiveXObject(name);
            return true;
        }catch(ex){
            return false;
        }
    }

    alert(hasIEPlugin("QuickTime.QuickTime"));
    
之所以要在try-catch语句中进行实例化，是因为创建未知COM对象会导致抛出错误。

### 兼容浏览器的检测方法
由于这两种检测的方法差别太大，因此典型的做法是针对每个插件分别创建检测函数。

    function hasFlash(){
        var result = hasPlugin("Flash");
        if(!result){
            result = hasIEPlugin("ShockwaveFlash.ShockwaveFlash");

        }return result;
    }

    function hasQuickTime(){
        var result = hasPlugin("QuickTime");
        if(!result){
            result = hasIEPlugin("QuickTime.QuickTime");
        }return result;
    }