---
layout: post
title: 变量对象
category: js
---
每个执行环境都有一个与之关联的变量对象，环境中定义的所有变量和函数都保存在这个对象中。

全局对象是在进入任何执行环境之前就已经创建的对象，这个对象只存在一份，它的属性在程序中任何地方都可以访问，全局对象的生命周期终止于程序退出那一刻。

arguments对象是活动对象的一个属性，它包含如下属性：

* callee 指向当前函数的引用
* length 真正传递参数的个数
* properties-indexes 该属性的值就是函数参数的值


每个函数在被调用时，其活动对象都会自动取得两个特殊变量：this和arguments。内部函数在搜索这两个变量时，只会搜索到期活动对象为止，因此不可能直接访问外部函数中的这两个变量。

    var name="The Window";

    var object = {
        name:"My Object",
        getNameFunc:function(){
            return function(){
                return this.name;//this 不能直接访问外部函数的对象object
            };
        }
    };

    alert(object.getNameFunc()());// The Window
    
当每个函数第一次被调用时，会创建一个执行环境及相应的作用域链，并把作用域链赋值给一个特殊的内部属性。然后使用this、arguments和其他命名参数的值来初始化函数的活动对象。

作用域链本质上是一个指向变量对象的指针列表，它只引用但不包含变量对象。

    function compare(value1,value2){
        if(value1<value2){
            return -1;
        }else if(value1 > vlaue2){
            return 1;
        }else{
            return 0;
        }
    }
    var result = compare(5,10);

当第一次调用compare()时，会创建一个包含this、arguments、value1和value2的活动对象。全局执行环境的变量对象包含this、result、compare在compare执行环境的作用域链中则处于第二位。