---
layout: post
title: ECMAScript 中的基本数据类型
---

ECMAScript中有5中基本数据类型——Undefined、Null、 Boolean、 Number和String，还有一种复杂数据类型——Object。所有值都是上述6中数据类型之一。

##检测数据类型之 typeof

    "undefined" 	 如果这个值未定义
    "boolean"		如果这个值是布尔值
    "string"		如果这个值是字符串
    "number"		如果这个值是数值
    "object"		如果这个值是对象或null
    "function"		如果这个值是函数

##数据类型之一 Undefined

Undefined类型只有一个值——undefined，引入这个值是为了区分空对象指针和未初始化的变量

使用var声明变量但未对其初始化时，这个变量的值就是undefined  var message；

未初始化的变量和未声明的变量执行typeof都返回undefined

没必要把一个变量的值显示的设为undefined

##数据类型之二 Null

Null类型只有一个值——null，null值表示一个空对象指针

如果定义的变量在将来用于保存对象，最好将该变量初始化为null，这样只要检查null就可以知道相应的变量是否已经保存了一个对象的引用了。

**alert(null==undefined);返回true**

##数据类型之三 Boolean

Boolean类型值true,false是区分大小写的

要将一个值转换为Boolean值，可调用函数Boolean()

| 数据类型 | 转换为true的值 |转换为false的值|
|--------|---------------|---------|
| Boolean       | true       |   false     |
|String|任何非空字符串|空字符串|
|  Number      |  任何非0数字包括无穷      |0和NaN|
|Object|任何对象|null|
|Undefined|/|undefined|

##数据类型之四 Number
虽然数值可以用八进制或十六进制来表示，但在进行算术计算时，所有以八进制和十六进制表示的数值**最终都将被转换成十进制**。
####浮点数值

保存浮点数值需要的内存空间是整数数值的两倍，因此ECMAScript会把浮点数转换为整数。

浮点数进行算术计算时其精确度远远不如整数，例如0.1+0.2的结果不是0.3而是0.30000000000000004。**这个小小的舍入误差会导致无法测试特定的浮点数值**。

####数值范围

最小数值保存在Number.MIN_VALUE中，最大数值保存在Number.MAX_VAlUE中

如果想确定一个数值是不是有穷的。可以使用函数isFinite()

	alert(isFinite(result));

访问Number.NAGATIVE_INFINTY和Number.POSITIVE_INFINITY可以得到正和负的Iifinity值

#### NaN
表示一个本来要返回数值的操作数未返回数值的情况，这样就不会抛出错误了，不会影响其他代码的执行

任何涉及NaN的操作都会返回NaN

NaN与任何值都不想等，包括NaN

isNaN()确定参数是否“不是数值”。isNaN接收到一个值之后，会尝试将这个值转换为数值，例如："10"或Boolean值。

基于对象调用isNaN()时，会首先调用valueof()方法，确定该方法返回的值是否可以转换为数值，如果不能基于这个返回值再调用toString方法，再测试返回值

#### 数值转换

#####Number()

* 可用于任何数据类型

* null值或空字符串返回0，undefined值返回NaN

* 如果是字符串遵循以下规则：

   - 字符串中只包含数字，将其转换为十进制数值，"011" 转换为11，会忽略前导0

   - 字符串中只包含有效的浮点格式，将其转换为对应的浮点数值，忽略前导0
   
   - 字符串中只包含有效的十六进制格式，将其转换为同样大小的十进制整数。
  
   - 字符串中包含数字之外的字符，将其转换为NaN。例如：Number("123da");//NaN
    
* 如果是对象，则调用valueOf(),返回的还是NaN再调用toString()

#####parseInt(要转换的数据，基数)

* 忽略字符串前面的空格，直至找到字符串中第一个非空格字符，第一个字符不是数字字符或负号就会返回NaN

* 转换空字符会返回NaN

* "22.5" 转换为22，因为小数点不是有效的数字字符

* 能识别各种整数格式，八进制、十六进制等。

		parseInt("070");//56

* 为避免错误的解析，建议无论什么情况下都明确指定基数（要转换的数是几进制）
        var num1=parseInt("AF",16)  //175,明确告诉parseInt要转换的是十六进制数
        var num2=parseInt("AF");		//NaN

#####parseFloat()

* 始终忽略前导0，十六进制格式的字符串始终转换成0

* "22.43.5"转换为22.34，第一个小数点有效，第二个小数点无效。

* 只解析十进制值，没有第二个参数

* 如果字符串包含的是可解析为整数的数，parseFloat会返回整数。

##数据类型之五 String

\xnn 以十六进制nn表示一个字符

\unnnn	以十六进制nnnn表示一个字符

转义字符，可以出现在字符串中任意位置，也将被作为一个字符来解析

alert(text.length)  //如果字符串中包含双字节字符，那么length属性可能不会精确的返回字符串中的字符数目

####toString()
* 返回相应值的字符串 

        var age=11; 
        var ageAsString=age.toString(); //字符串"11"

* null和undefined没有这个方法

* 通过传递基数，toString可以输出以二进制、八进制、十进制、十六进制等有效进制格式的字符串值

        var num=10;
        alert(num.toString(2)); //"1010"
        
            
* 不知道转换的值是不是null或undefined的情况下，可以使用String方法，这个函数可以将任何类型的值转换为字符串值,并且遵循下列转换规则：
  - 如果值有toString()方法，则调用该方法，返回相应的字符串
  
  - 如果值是null，则返回"null"
 
  - 如果值是undefined，则返回"undefined"

##数据类型之六 Object

**Object的每个实例都具有以下方法和属性：**

* constructor——保存着用于创建当前对象的函数

* hasOwnProperty(propertyName)——检查给定的属性在当前对象中是否存在  o.hasOwnProperty("name")

* propertyIsEnumberable(propertyName)——检查给定的属性是否能用for-in语句来枚举

* isPrototypeOf(object)——检查传入的对象是否是另一个对象的原型

* toString——返回对象的字符串表示

* valueOf()——返回对象的字符串、数值或布尔值表示

* IE的JS实现在对象方面稍有不同，只有开发人员定义的对象才继承自object，所有BOM和DOM对象也与这里介绍的不同，可能不会具有object的所有属性和方法。