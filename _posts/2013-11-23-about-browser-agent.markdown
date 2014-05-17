---
author: admin
comments: true
date: 2013-11-23 09:01:17+00:00
layout: post
category: js
title: 兼容所有浏览器的用户代理检测

---

用户代理检测是客户端检测中的一种，主要是检测呈现的引擎。
呈现引擎分五大类：IE、Opera、Gecko、WebKit、KHTML



    
    var client=function(){//创建一个对象
    				var engine={//初始化engine对象
    						ie:false,//确定是否是ie引擎
    						gecko:false,
    						webkit:false,
    						khtml:false,
    						opera:false,
    						ver:0//引擎的版本
    				};  
    				var browser={
    						ie:false,
    						firefox:false,
    						opera:false,
    						chrome:false,
    						safari:false,
    						ver:0,
    						name:''//浏览器的通用名称
    				};
    				var system={
    						win:false,
    						mac:false,
    						x11:false,
    						sysname:''
    				};
    				var ua=navigator.userAgent;
    				var p=navigator.platform;
    
    				if(p.indexOf('Win')==0){
    						system.win=true;
    						system.sysname='windows';
    					}else if(p.indexOf('Mac')==0){
    							system.mac=true;
    							system.sysname='mac';
    					}else if(p=='X11'||p.indexOf('Linux')==0){
    							system.x11=true;
    							system.sysname='Linux';
    					}
    
    				if(window.opera){
    						engine.opera=browser.opera=true;
    						engine.ver=browser.ver=window.opera.version();
    						browser.name="opera";
    				}else if(/AppleWebKit\/(\S+)/.test(ua)){
    						engine.webkit=true;
    						engine.ver=browser.ver=RegExp['$1'];
    						if(/Chrome\/(\S+)/.test(ua)){
    						browser.name='chrome';
    						browser.ver=RegExp['$1'];
    						browser.chrome=true;
    						}
    						else{
    							browser.name='safari';
    							if(/Version\/(\S+)/.test(ua)) browser.ver=RegExp['$1'];
    							browser.safari=true;
    						}
    
    				}
    				else if(/KHTML\/(\S+)/.test(ua)||/konqueror\/([^;]+)/.test(ua)){
    						engine.ver=RegExp['$1'];
    						engine.khtml=true;
    				}
    				else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){//根据版本来写正则表达式
    						engine.ver=RegExp['$1'];
    						engine.gecko=true;
    						if(/Firefox(\S+)/.test(ua)){
    								browser.ver=RegExp['$1'];
    								browser.firefox=true;
    								browser.name='Firefox';
    						}
    
    				}
    				else if (/MSIE([^;]+)/.test(ua))
    				{
    						engine.ver=browser.ver=RegExp['$1'];
    						engine.ie=browser.ie=true;
    						browser.name='ie';
    				}
    				return {//返回一个对象
    					engine:engine,
    					browser:browser,
    					system:system
    
    				}
    		}();
        document.write(navigator.userAgent+'
    ');
    	document.write(navigator.platform);
    	alert(client.system.sysname+client.browser.name+client.browser.ver);
