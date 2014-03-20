---
layout: post
title: 引用类型之一 Object
---
引用类型的值是引用类型的一个实例。

引用类型描述的是一类对象所具有的属性和方法。

## 创建Object对象的实例 
### 字面量方法

    var person = {
        name:"Nicholas",//属性名也可以加引号
        age:29//最后一个属性不能加逗号
    };

在通过对象字面量定义对象时，实际上不会调用Object构造函数。（Firefox除外）

    function displayInfo(args){
        var output = " ";
        if(typeof args.name == "string"){
            output += "Name:"+ args.name + "\n";
        }
        if(typeof args.name == "number"){
            output+= "Age:"+args.age + "\n";
        }
        alert(output);
    }

    displayInfo({name:"Nichiloa",age:29});
    displayInfo({name:"Gref"});
    
这个例子中，函数displayInfo()接受一个名为args 的参数，这个参数可能带有一个名为name或age的属性，也可能这两个属性都有或者都没有。在这个函数内部，我们通过typeof操作符来检测每个属性是否存在。调用了两次这个函数，每次都使用一个对象字面量来指定不同的数据，两次传递的参数不同，但都能正常执行。

这种传递参数的模式最适合需要向函数传入大量可选参数的情形。一般来讲，命名参数虽然容易处理，但在有多个可选参数的情况下就会显示不够灵活。最好的做法是对那些必须的值使用命名参数，而使用对象字面量来封装对个可选参数。



### 构造函数方法

    var person = new Object();
    person.name = "me";
    person.age = 20;
    
## 访问对象属性

    alert(person.name);
    alert(person["name"]);//属性必须以字符串的形式放入
    
方括号语法的主要优点是可以通过变量来访问属性。哈希表中使用的就是这种方法来存放和访问字母的出现次数。