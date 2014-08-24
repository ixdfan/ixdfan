---
layout: post
title: 闭包
category: js
---
##什么是闭包
闭包是有权访问另一个函数作用域中的变量的函数

## 闭包的使用

### 为什么需要闭包

    function func(){
        var a = 1;
        a++;
        alert(a);

    }

    func();//2  调用完func后，a就被销毁了，下一次调用时，重新把a初始化为1
    func();//2
    
如果想让a的值每次调用能实现累加效果，也就是第二次调用时弹出3，这就需要闭包。

在函数func()内部定义的变量是局部变量，在函数外部无法访问。但是有时候又需要在函数func()外部访问它的局部变量，怎么办呢，就在func()内部再定义一个函数innerFunc()，在innerFunc()中可以访问函数func()的局部变量,因为innerFunc()的作用域链中包含func()的作用域。

	function func(){
    	var a = 1;
        function innerFunc(){
         alert(a++);        
        }
    return innerFunc;//如果不返回innerFunc，innerFunc就是func函数的局部变量，不能在函数外部访问
    }
    
    var reslut = func();//func执行完后，它的局部变量依然在内存中，不会立即被销毁
    result();//1 在func()外部访问到了它的局部变量a
    result();//2 变量a
    result = null;//解除对func的引用以便释放内存

func()函数执行完毕后，其活动对象也不会被销毁，因为innerFunc函数的作用域链任然在引用这个活动对象，直到innerFunc被销毁后，func的活动对象才会被销毁。



### 闭包的作用
* 访问函数内部的局部变量

* 让这些局部变量始终保存在内存中

### 闭包的缺点
* 闭包会携带包含它的函数的作用域，因此会比其它函数占用更多的内存，过渡使用闭包可能会导致内存占用过多

* 闭包会引用包含它的函数的活动对象，因此会导致其无法被及时销毁

### 闭包与变量

闭包只能取得包含函数中任何变量的最后一个值。

    function createFunction(){
        var result = new Array();
        for(var i = 0 ; i < 10; i++){
            result[i] = function(){
                return i;//引用createFunction中的局部变量i
            }

        }//执行完for循环后局部变量i 的值为10
        return result;
    }
    var funcs = createFunction();//执行完createFunction函数后，它的活动对象并没有被销毁，此时的i=10
    for(var i = 0 ; i< funcs.length; i++){
        document.write(funcs[i]());//全都输出10  运行createFunction中的匿名函数时，其中的i 都引用的是同一局部变量i
    }
    
重写闭包，让每个函数都返回自己的索引值

    function createFunction(){
        var result = new Array();
        for(var i = 0; i< 10; i++){
            result[i]=function(num){
                return function(){
                    return num;//
                };
            }(i);//函数参数是按值传递的，即将i的当前值复制给参数num
        }return result;
    }
    var funcs= createFunction();
    for(var i = 0; i< 10;i++){
        document.write(funcs[i]());//分别返回各自不同的索引值
    }
    

###闭包中的this

在全局函数中this=window,当函数被当做某个对象的方法调用时，this等于那个对象。匿名函数的执行环境具有全局性，因此其this通常指向window

    var name = "The Window";

    var object = {
        name:"My Object",
        getNameFunc:function(){
            return function(){
            return this.name;
            };
        }
    };

    alert(object.getNameFunc()());//The Window

内部函数在搜索this和arguments这两个变量时，只会搜索到其活动对象为止，因此永远不可能直接访问外部函数的这两个变量。如果想访问外部函数的这两个变量，必须将该变量的引用保存到另一个闭包能访问的变量中。

###内存泄露

由于IE对JScipt对象和COM对象使用不同的垃圾收集例程，因此闭包在IE中会导致一些特殊的问题。如果闭包的作用域链中保存着一个HTML元素，那么就意味着该元素将无法被销毁。

    function assignHandler(){
        var element = document.getElementById("someElement");
        element.onclick = function(){
            alert(element.id);
        };
    }

匿名函数中保存了一个对assignHandler的活动对象的引用，因此就会导致无法减少element的引用数。只要匿名函数存在，element的引用数至少也是1，因此他所占用的内存就永远不会被回收。

为了避免这样的问题，将其改写为下面的形式

    function assignHandler(){
        var element = document.getElementById("someElement");
        var id = element.id;//把element.id的一个副本保存在一个变量中，并且在闭包中引用该变量消除了循环引用
        element.onclick=function(){
            alert(id);
        };
        element = null;//解除对DOM对象的引用，减少引用次数，确保正常回收其占用的内存。
    }

闭包会引用外部函数的整个活动对象，而其中包含着element。即使闭包不直接引用element，包含函数的活动对象中也仍然会保存一个引用。