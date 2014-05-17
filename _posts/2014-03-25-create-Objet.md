---
layout: post
title: 创建对象
category: js
---
## 原始方式

    var person = new Object();
    
    person.name = "Ni";
    person.age = 10;
    person.sayName = function(){
        alert(this.name);
    };
    
    person.sayName();//Ni

使用这种方法创建对个相似对象，会产生大量重复的代码，为了解决这个问题，出现了工厂模式。

## 工厂模式

    function createObj(name,age){
        var obj = new Object();

        obj.name = name;
        obj.age = age;
        obj.sayName = function(){
            alert(this.name);
        }

        return obj;
    }
	var obj = createObj("NI",12);
    obj.sayName();//Ni
    
用函数来封装创建特定对象的过程，通过调用函数来创建多个相似的对象，但是所有对象都是Object类型的，不能判断对象的具体类型。于是又出现了构造函数模式

## 构造函数模式

    function Person(name,age){
        this.name = name;
        this.age = age;
        this.sayName = function(){
            alert(this.name);
        };
    }

    var person1 = new Person("Ni",12);
    person.sayName();//Ni
    alert(person1.constructor == Person);//true
    alert(person1 instanceof Object);//true 所有对象都继承自Object
    alert(person1 instanceof Person);//true 检测对象类型

person1实例有一个constructor属性，该属性指向Person。

通过instanceof 来检测对象的类型

创建自定义的构造函数意味着将来可以将它的实例标识为一种特定的类型，这正是构造函数模式胜过工厂模式的地方。

**要创建Person的实例，必须使用new操作符，以这种方式调用构造函数实际上会经历以下四个步骤：**

* 创建一个新对象

* 将构造函数的作用域赋给新对象，因此this就指向了这个新对象

* 执行构造函数中的代码，为这个新对象添加属性和方法

* 返回新对象

**构造函数与工厂模式的不同：**

* 没有显示的创建对象

* 直接将属性和方法赋给了this对象

* 没有return 语句

### 构造函数返回引用类型

    var obj = new function(){return "abc";};
    alert(obj);//[Object Object]

	//当构造函数返回值是引用类型时，返回值会覆盖掉新创建的对象
    var obj = new function(){return new String("abc");}
    alert(obj);//abc

### 将构造函数当做函数

构造函数和其他函数唯一的区别是调用他们的方式不同。

任何函数只要通过new操作符来调用，就可以作为构造函数，任何构造函数不通过new操作符来调用它就是普通函数。

**当做构造函数使用**

    var person2 = new Person("si",23);
    person.sayName();//si

**当做普通函数使用，在全局作用域中调用Person函数，因此函数中的this就等于window，方法就被添加到window上**

    Person("hi",23);
    window.sayName();//hi 

**在另一个对象的作用域中调用**

    var obj = new Object();
    Person.call(obj,"mi",23);
    obj.sayName();//mi

### 构造函数模式的缺点

每个方法都要在每个实例上重新创建一遍

为了解决这个问题，把方法定义转移到函数外部

    function Person(name,age){
        this.name = name ;
        this.age = age ;
        this.sayName = sanName；//sayName是指向函数的一个指针，因此每个实例都是引用的同一个函数
    }

    function sayName(){
        alert(this.name);
    }

如果要定义很多方法，就要定义很多全局函数，而且这些全局函数只能被特定的对象调用。于是就出现了原型模式

## 原型模式

    function Person(){}

    Person.prototype.name = "Ni";
    Person.prototype.age = 12;
    Person.sayName = function(){
        alert(this.name);
    };

    var person1 = new Person();
    person1.sayName();//Ni
    
    var person2 = new Person();
    person2.sayName();//Ni
    
    //检测name属性是否是person2的实例属性
    alert(person2.hasOwnProperty("name"));//false
    
    //检测name属性是否存在实例属性或原型属性中
    alert("name" in person2);true
    
    
创建的每个函数都有一个prototype属性，这个属性是一个对象，这个对象时所有实例共享的，所以可以将实例共享的属性和方法添加到原型对象中。

使用原型的特点是，可以让所有实例共享它所包含的属性和方法。

hasOwnProperty()方法，检测属性是否是实例属性，是实例属性则返回true

单独使用in操作符会在通过对象能访问给定属性时返回true，无论该属性在原型中还是实例中。

**可以把原型模式写得更简洁：**

    function Person(){}
    
    //将Person.prototype设置为等于一个以字面量创建的新对象，constructor属性不再指向Person了，所有需要重新指定constructor属性
    Person.prototype = {
    	constructor：Person，
        name: "Ni",
        age: 23,
        sayName:function(){
            alert(this.name);
        }
    };

调用构造函数时会为实例添加一个指向最初原型的_proto_指针，而把原型修改为另一个对象就等于切断了构造函数与最初原型之间的联系。

实例中的指针只指向原型，而不指向构造函数。

重写原型对象切断了现有原型与任何之前已经存在的对象实例之间的联系，因为他们引用的仍然是最初的原型。如果实例是在重写原型之后创建的，那么不会有影响。

	//可以像修改自定义的原型一样修改原生对象的原型，因此可以随时添加方法。
    String.prototype.special = function(text){
        return this.indexOf(text) == 0;
    }

    var message = "Hello world";
    alert(message.special("Hello"));//true

方法被添加给了String.prototype，那么当前环境中的所有字符串都可以调用它。

这样修改原生对象的原型，可能导致命名冲突，或者重写原生方法。

#### 原型对象的问题

所有实例在默认情况下都取得相同的属性值，包含基本类型值的属性可以在实例中通过重写该属性来取得实例特有的值，但是对包含引用类型值的属性，改变一个实例中的引用类型值，所有实例都共享了修改后的引用类型值。

    function Person(){}

    Person.prototype = {
        name:"Ni",
        fridend:["A","B"],
        sayName:function(){
            alert(this.name);
        }

    };

    var person1 = new Person();
    var person2 = new Person();

    person1.name = "Si";
    person1.sayName();//Si

    person1.friends.push("C");
    alert(person2.fridens);//A,B,C

## 组合使用构造函数模式和原型模式
	//在构造函数中定义实例属性
    function Person(name,age){
        this.name = name;
        this.age = age;
        this.friends = ["a","b"];

    }

	//在原型中定义实例共享的方法和属性
    Person.prototype = {
        constructor: person,
        sayName:function(){
            alert(this.name);
        }

    };

    var person1 = new Person("Ni",12);
    var person2 = new Person("Si",23);

    person1.sayName();//Ni
    person2.sayName();//Si

    person1.friends.push("c");
    alert(person1.friends);//a,b,c
    alert(person2.friends);//a,b

这种方式创建实例，每个实例都有自己的一份实例属性的副本，同时又共享这方法的引用，最大限度的节省了内存，还支持向构造函数传递参数。但是并没有把所有信息都封装在构造函数中。于是就有了动态原型模式。

## 动态原型模式

    function Person(name,age){
        this.name = name;
        this.age = age;

		//只在sayName()不存在时将它添加到原型中
        if(typeof this.sayName != "function"){
        
        //只在初次调用构造函数时才会执行
            Person.prototype.sayName = funcition(){
                alert(this.name);
            };
        }
    }

if语句检查的可以是初始化之后应该存在的任何属性或方法，只要检测其中一个即可。

## 寄生构造函数模式

    function SpecialArray(){
        var  values = new Array();
        
        //在values对象中调用push，并传参arguments ，初始化values
        values.push.apply(values,arguments);
        values.toSpecialString = function(){
            return this.join("|");
        };

        return values;
    }

    var colors = new SpecialArray("red","blue","green");
    alert(colors.toSpecialString());//red | blue |green

除了使用new操作符并把使用的包装函数叫做构造函数外，这个模式跟工厂模式是一样的。

这个模式可以在特殊的情况下用来为对象创建构造函数。如果想创建一个具有特殊方法的数组，由于不能直接修改Array构造函数，因此可以使用这个模式。

这个模式返回的对象与构造函数或构造函数的原型属性之间没有关系，因此不能用instanceof来确定对象的类型。

## 稳妥构造函数模式

    function Person(name,age){
        var obj = new Object();

        //传进来的参数name，只有用sayName()方法才能访问
        obj.sayName = function(){
            alert(name);
        };

        return obj;
    }
	
    var person1 = new Person("Ni",23);
    person1.sayName();//Ni
    
除了使用sayName()方法之外，没有其他的办法访问name的值。

变量person1中保存的是一个稳妥对象，而除了sayName方法外，没有别的方式可以访问其数据成员。

稳妥构造函数模式提供的这种安全性，使得它非常适合在某些安全执行环境。

使用稳妥构造函数模式创建的对象与构造函数之间也没有什么关系，因此instanceof操作符对这种对象也没有意义。























