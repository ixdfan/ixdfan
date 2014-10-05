---
layout: post
title: setTimeout
category: js
---
## 常见实例

### JS是单线程的，空闲时才执行setTimeout

    (function(){
        setTimeout(funciton(alert("settimeout")),0);
        alert("normal");
    })();
    alert(2);
    //弹出顺序 normal-->2-->settimeout

原因：

JS是单线程的，所以setTimeout需要等JS空闲才会执行，即使setTimeout设置的时间间隔为0，也要等到该线程执行完才执行。

### alert暂停当前脚本，会影响setTimeout的执行顺序

    var len=4;
    while(len--){
        setTimeout(function(){ alert(len); },0);
        alert(len); 
        }//理论弹出顺序 3 2 1 0 -1 -1 -1 -1，但是实际不是按照这个顺序弹出，每次的顺序可能都不一样。
        
原因：

alert会暂停进程，会影响setTimeout的执行顺序，所以每次的顺序可能不一样，用console.log来查看就不会有这样的问题了。



