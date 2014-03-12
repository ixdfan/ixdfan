---
layout: post
title: ECMAScript 中的基本数据类型
---

ECMAScript中有5中基本数据类型——Undefined、Null、 Boolean、 Number和String，还有一种复杂数据类型——Object。所有值都是上述6中数据类型之一。
##检测数据类型之 typeof

"undefined" 如果这个值未定义
"boolean"		如果这个值是布尔值
"string"			如果这个值是字符串
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

alert(null==undefined);返回true

##数据类型之三 Boolean

Boolean类型值true,false是区分大小写的

要将一个值转换为Boolean值，可调用函数Boolean()

##数据类型之四 Number

####浮点数值

保存浮点数值需要的内存空间是整数数值的两倍，因此ECMAScript会把浮点数转换为整数。

浮点数进行算术计算时其精确度远远不如整数，例如0.1+0.2的结果不是0.3而是0.30000000000000004

####数值范围

最小数值保存在Number.MIN_VALUE中，最大数值保存在Number.MAX_VAlUE中

确定数值是否有穷用函数isFinite()

访问Number.NAGATIVE_INFINTY和Number.POSITIVE_INFINITY可以得到正和负的Iifinity值

#### NaN
表示一个本来要返回数值的操作数未返回数值的情况，这样就不会抛出错误了，不会影响其他代码的执行

任何涉及NaN的操作都会返回NaN

NaN与任何值都不想等，包括NaN

isNaN()确定参数是否“不是数值”

基于对象调用isNaN()时，会首先调用valueof()方法，确定该方法返回的值是否可以转换为数值，如果不能基于这个返回值再调用toString方法，再测试返回值

#### 数值转换

#####Number()

* 可用于任何数据类型

* null值或空字符串返回0，undefined值返回NaN

* 只包含数字的字符串，将其转换为十进制数值，"011" 转换为11

* 包含有效十六进制格式的字符串，转换为相同大小的十进制整数值

#####parseInt(要转换的数据，基数)

* 忽略字符串前面的空格，直至找到字符串中第一个非空空格，如果第一个字符不是数字字符或负号就会返回NaN

* 为避免错误的解析，建议无论什么情况下都明确指定基数
        var num1=parseInt("AF",16)  //175
        var num2=parseInt("AF");		//NaN

#####Float()

* 忽略前导0，十六进制格式的字符串始终转换成0

* 析十进制值，没有第二个参数

##数据类型之五 String

\xnn 以十六进制nn表示一个字符

\unnnn	以十六进制nnnn表示一个字符

alert(text.length)  //如果字符串中包含双字节字符，那么length属性可能不会精确的返回字符串中的字符数目

####string
* 返回相应值的字符串 

        var age=11; 
        var ageAsString=age.toString(); //字符串"11"

* null和undefined没有这个方法

* 通过传递基数，toString可以输出以二进制、八进制、十进制、十六进制等有效进制格式的字符串值

        var num=10;
        alert(num.toString(2)); //"1010"
        
            
* 不知道转换的值是不是null或undefined的情况下，可以使用String方法，这个函数可以将任何类型的值转换为字符串值

##数据类型之六 Object

**Object的每个实例都具有以下方法和属性：**

* constructor——保存着用于创建当前对象的函数

* hasOwnProperty(propertyName)——检查给定的属性在当前对象中是否存在  o.hasOwnProperty("name")

* propertyIsEnumberable(propertyName)——检查给定的属性是否能用for-in语句来枚举

* isPrototypeOf(object)——检查传入的对象是否是另一个对象的原型

* toString——返回对象的字符串表示

* valueOf()——返回对象的字符串、数值或布尔值表示

* IE的JS实现在对象方面稍有不同，只有开发人员定义的对象才继承自object，所有BOM和DOM对象也与这里介绍的不同，可能不会具有object的所有属性和方法。