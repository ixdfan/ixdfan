---
layout: post
title: 客户端检测之用户代理检测
category: js
---
用户代理检测通过检测用户代理字符串来确定实际使用的浏览器。

在每一次HTTP请求过程中，用户代理字符串是作为响应首部发送的，而且该字符串可以通过JS的navigator.userAgent属性访问。

**电子欺骗**：浏览器通过在自己的代理字符串中加入一些错误或误导性信息，来达到欺骗服务器的目的。

大多数浏览器为了不被一些站点拒之门外，向用户代理字符串中放入足够多的信息，以便站点能信任它与其他流行的浏览器是兼容的。所以检测特定的浏览器就变得异常麻烦。

## 用户代理检测技术
### 识别呈现引擎

确切知道浏览器的名字和版本号不如确切的知道它使用的是什么呈现引擎。因为如果浏览器支持的是相同版本的呈现引擎，那他们一定支持相同的特性。

因此，我们编写的脚本主要检测5大呈现引擎：IE、Gecko、WebKit、KHTML和Opera

为了不在全局作用域中添加多余的变量，使用模块增强模式来封装检测脚本。

    var client = function(){
        var engine = {//呈现引擎
            ie:0,
            gecko:0,
            webkit:0,
            khtml:0,
            opera:0,
            ver:null;//具体的版本
        };
		
        
        var ua = navigator.userAgent;
        //检测window.opera对象识别opera引擎
        if(window.opera){
            engine.ver = window.opera.version();
            engine.opera = parseFloat(engine.ver);
        }
        
        //检测用户代理字符串中AppleWebKit字符串识别webkit
        else if(/AppleWebKit\/(\S+)/.test(ua)){
            engine.ver = RegExp["$1"];
            engine.webkit = parseFloat(engine.ver);
        }
        
        //检测KHTML字符串识别khtml
        else if(/KHTML\/(\S+)/.test(ua)||/Konqueror\/([^;]+)/.test(ua)){
            engine.ver = RegExp["$1"];
            engine.khtml = parseFloat(engine.ver);
        }
        
        //检测rv: 识别gecko
        else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){
            engine.ver = RegExp["$1"];
            engine.gecko = parseFloat(engine.ver);
        }
        
        //检测MSIE识别ie
        else if(/MSIE ([^;]+)/.test(ua)){
            engine.ver  = browser.ver = RegExp["$1"];
            engine.ie = parseFloat(engine.ver);
        }
        
        return {
            engine:engine,
        };
    }();

要识别opera，必须的检测window.opera对象，调用其version()方法会返回一个表示浏览器版本的字符串。

WebKit的用户代理字符串中的"AppleWebKit"是独一无二的，因此检测这个字符串最合适。

检测顺序：opera-->webkit-->khtml-->gecko-->ie

## 识别浏览器
不同的浏览器使用相同的呈现引擎，使用不同的JS引擎，因此需要判断浏览器

为client变量添加一些新的属性，添加一个私有变量browser,用于保存每个主要浏览器的属性。

 var client = function(){
        var engine = {//呈现引擎
            ie:0,
            gecko:0,
            webkit:0,
            khtml:0,
            opera:0,
            ver:null;//具体的版本
        };
        
        var browser = {//浏览器
        	ie:0,
            firefox:0,
            safari:0,
            chrome:0,
            opera:0,
            konq:0,
            ver:null
            
        };
		
        
        var ua = navigator.userAgent;
        //检测window.opera对象识别opera引擎
        if(window.opera){
            engine.ver =browser.ver= window.opera.version();
            engine.opera = browser.opera=parseFloat(engine.ver);
        }
        
        //检测用户代理字符串中AppleWebKit字符串识别webkit
        else if(/AppleWebKit\/(\S+)/.test(ua)){
            engine.ver = RegExp["$1"];
            engine.webkit = parseFloat(engine.ver);
            
            //通过Chorme判断Chrome浏览器
            if(/Chrome\/(\S+)/.test(ua)){
            	browser.ver = RegExp["$1"];
                browser.chrome = parseFloat(browser.ver);
            }
            
            //通过Version判断safari浏览器
            else if(/Version\/(\S+)/.test(ua)){
            	browser.ver = RegExp["$1"];
                browser.safari = parseFloat(browser.ver);
            }
        }
        
        //检测KHTML字符串识别khtml
        else if(/KHTML\/(\S+)/.test(ua)||/Konqueror\/([^;]+)/.test(ua)){
            engine.ver = browser.ver = RegExp["$1"];
            engine.khtml = browser.konq = parseFloat(engine.ver);
        }
        
        //检测rv: 识别gecko
        else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){
            engine.ver = RegExp["$1"];
            engine.gecko = parseFloat(engine.ver);
            
            if(/Firefox\/(\S+)/.test(ua)){
            	browser.ver = RegExp["$1"];
                browser.firefox = parseFloat(browser.ver);
            }
        }
        
        //检测MSIE识别ie
        else if(/MSIE ([^;]+)/.test(ua)){
            engine.ver  = browser.ver = RegExp["$1"];
            engine.ie = browser.ie= parseFloat(engine.ver);
        }
        
        return {
            engine:engine,
            browser:browser
        };
    }();

##识别平台
在某些条件下，平台可能是必须关注的问题。

那些具有各种平台版本的浏览器再不同的平台下可能会有不同的问题。

目前三大主流平台：Windows、Mac和Unix（包括各种Linux）

为了检测平台需要添加一个新对象

    var system = {//平台
        win:false,
        mac:false,
        xll:false
    };


    //检测平台
    var p = navigator.platform;
    system.win = p.indexOf("Win")==0;
    system.mac = p.indexOf("Mac")==0;
    system.xll = (p.indexOf("Xll")==0)||(p.indexOf("Linux")==0);
    
navigator.platform在不同浏览器中会给出不同的平台信息

## 识别windows 操作系统
## 识别移动设备

    var system = {
        iphone:false,
        ipod:false,
        nokiaN:false,
        winMobile:false,
        macMobile:false
    };

    system.iphone = ua.indexOf("iphone")>-1;
    system.ipod = ua.indexOf("iPod")>-1;
    system.macMobile = (system.iphone||system.ipod);
    system.nokiaN = ua.indexOf("NokiaN")>-1;
    system.winMobile = (system.win=="CE");

##识别游戏系统

    var system = {
        wii:false,
        ps:false
    };

    system.wii = ua.indexOf("Wii")>-1;
    system.ps = /playstation/i.test(ua);

## 完整的代码
 var client = function(){
        var engine = {//呈现引擎
            ie:0,
            gecko:0,
            webkit:0,
            khtml:0,
            opera:0,
            ver:null;//具体的版本
        };
        
        var browser = {//浏览器
        	ie:0,
            firefox:0,
            safari:0,
            chrome:0,
            opera:0,
            konq:0,
            ver:null
            
        };
        
        var system = {//平台
        win:false,
        mac:false,
        xll:false,
        
        iphone:false,
        ipod:false,
        nokiaN:false,
        winMobile:false,
        macMobile:false,
        
        wii:false,
        ps:false
        
    };
		
        
        var ua = navigator.userAgent;
        //检测window.opera对象识别opera引擎
        if(window.opera){
            engine.ver =browser.ver= window.opera.version();
            engine.opera = browser.opera=parseFloat(engine.ver);
        }
        
        //检测用户代理字符串中AppleWebKit字符串识别webkit
        else if(/AppleWebKit\/(\S+)/.test(ua)){
            engine.ver = RegExp["$1"];
            engine.webkit = parseFloat(engine.ver);
            
            //通过Chorme判断Chrome浏览器
            if(/Chrome\/(\S+)/.test(ua)){
            	browser.ver = RegExp["$1"];
                browser.chrome = parseFloat(browser.ver);
            }
            
            //通过Version判断safari浏览器
            else if(/Version\/(\S+)/.test(ua)){
            	browser.ver = RegExp["$1"];
                browser.safari = parseFloat(browser.ver);
            }
        }
        
        //检测KHTML字符串识别khtml
        else if(/KHTML\/(\S+)/.test(ua)||/Konqueror\/([^;]+)/.test(ua)){
            engine.ver = browser.ver = RegExp["$1"];
            engine.khtml = browser.konq = parseFloat(engine.ver);
        }
        
        //检测rv: 识别gecko
        else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){
            engine.ver = RegExp["$1"];
            engine.gecko = parseFloat(engine.ver);
            
            if(/Firefox\/(\S+)/.test(ua)){
            	browser.ver = RegExp["$1"];
                browser.firefox = parseFloat(browser.ver);
            }
        }
        
        //检测MSIE识别ie
        else if(/MSIE ([^;]+)/.test(ua)){
            engine.ver  = browser.ver = RegExp["$1"];
            engine.ie = browser.ie= parseFloat(engine.ver);
        }
        
        //检测平台
    var p = navigator.platform;
    system.win = p.indexOf("Win")==0;
    system.mac = p.indexOf("Mac")==0;
    system.xll = (p.indexOf("Xll")==0)||(p.indexOf("Linux")==0);
    
    system.iphone = ua.indexOf("iphone")>-1;
    system.ipod = ua.indexOf("iPod")>-1;
    system.macMobile = (system.iphone||system.ipod);
    system.nokiaN = ua.indexOf("NokiaN")>-1;
    system.winMobile = (system.win=="CE");
    
     system.wii = ua.indexOf("Wii")>-1;
    system.ps = /playstation/i.test(ua);
        
        return {
            engine:engine,
            browser:browser,
            system:system
        };
    }();
