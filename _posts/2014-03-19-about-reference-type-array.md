---
layout: post
title: 引用类型之二 Array
category: js
---
数组的每一项都可以保存任何类型的数据。数组的大小是可以动态调整的，可以随着数据的增加自动增长以容纳新数据

##创建数组
### 1.使用构造函数

    var colors = new Array();
    var colors = new Array("res",10,true);
    var colors = new Array(10);//只传入一个参数用来指定数组的长度

也可以省略new操作符

### 2.字面量方法

    var colors = [,,];//创建一个包含2或3项的数组
    
    
IE的ECMAScript实现在数组字面量方面存在bug，导致这个数组包含3个项。

省略值的情况下，每一项都将获得undefined值

在使用字面量方法创建数组时，不会调用Array()构造函数（Firefox除外）

### 3.字符串生成数组

调用字符串对象的`split()`方法也可以生成数组

	var str = 'a b c';
    var arr = str.split(' ');
    print(arr)//[a,b,c]

## 数组项数
数组的项数保存在其length属性中，这个属性始终会返回0或更大值

数组的length属性，不是只读的，通过设置这个属性可以从数组的末尾添加或移除项。

    var colors = ["red","blue","green"];
    colors.length = 2;//数组长度设置为2，移除最后一项
    alert(colors[2]);//undefined

如果将其length属性设置为大于数组项的值，则新增的每一项都会取得undefined值。

    var colors = ["red","blue","green"];
    colors[colors.length] = "black";//在位置3添加一种颜色，添加后数组的长度变为4
    colors[colors.length] = "brown";//在位置4添加一种颜色
    
每当数组末尾添加一项后，其length属性都会自动更新以反应这个变化

当把一个值放在超出当前数组大小的位置上时，数组就会重新计算其长度值，即长度值等于最后一项的索引加1.

    var colors = ["red","green"];
    colors[99] = "black";
    alert(colors.length);//100
    
该数组从位置3到位置98的每一项都获得undefined

##操作方法

###1.转换方法
####toLocalString() toString() valueOf()

调用数组的**toString()**和**valueOf()**方法会返回相同的值，即由数组中的每个值的字符串形式拼接而成的一个以逗号分隔的**字符串**。

**toLocalString()**经常也会返回与toString()和valueOf()方法相同的值，不过为了取得每一项的值，调用的是每一项的toLocalString()方法。

    var colors = ["red","green","blue"];
    alert(colors.toString());//red,blue,green
    alert(colors.valueOf());//red,blue,green
    alert(colors);//red,green,blue
    
由于alert要接收字符串参数，所以她会在后台调用toString()方法，由此会得到与直接调用toString()方法相同的结果。

#### join()
只接受一个参数，即用作分隔符的字符串，然后返回包含所有数组项的字符串。

    var colors = ["red","blue","green"];
    alert(colors.join("||"));//red||blue||green
    alert(colors.join("x"));//redxbluexgreen
    
使用join()可以使用不同的分隔符来构建这个字符串。

如果数组中的某一项是null或undefined，那么该值在join()、toString()、toLocalString()、valueOf()方法返回的结果中以空字符串表示

###2.增删操作

#### 栈方法

栈是一种LIFO（last in first out）的数据结构，也就是最新添加的项最早被移除

栈中的插入和移除只会发生在栈的顶部

#####push()
接收任意数量的参数，把他们逐个添加到数组末尾，并**返回修改后数组的长度**

##### pop()
从数组末尾移除最后一项，减少数组的length值，并**返回移除的项**

    var colors = new Array();
    var count = colors.push("red","green");向数组中添加两项
    alert(count);//2

    count = colors.push("black");向数组中添加一项
    alert(count);//3返回修改后数组的长度

    var item = colors.pop();//移除数组的最后一项
    alert(item);//black 返回被移除的项

    alert(colors.length);//2 修改后数组的长度
    
####队列方法
队列数组结构的访问规则是FIFO（first in first out）

####shift()
移除数组中的**第一项并返回移除的项**，同时数组的长度减1

#### unshift()

在数组**前端添加**任意项并**返回新数组的长度**

    var colors = new Array();
    var count = colors.unshift("red","green");
    var count = colors.unshift("black");
    alert(colors);//black,red,green

    var item = colors.shift();
    alert(item);//black

IE中unshift()总是返回undefined而不是数组想新长度。

#### 任意位置增删元素

##### splice()

接收三个参数：起始索引、需要删除的元素个数、要添加进数组的元素

	var nums = [1,2,3,4,5];
    nums.splice(1,1,6,7);//在nums数组的位置1处删除一个元素，并且插入元素6,7
    print(nums);//[1,6,7,3,4,5]

###重排序方法
#### reverse()
反转数组项的顺序

    var values = [1,2,3,4,5];
    values.reverse();
    alert(values);//5,4,3,2,1
    
#### sort()
按升序排列数组项

sort()方法会调用每个数组项的toString()转型方法，然后比较得到的字符串，以确定如何排序。即使数组中每一项都是数值，sort()方法比较的也是字符串

    var values = [0,1,5,15,10];
    values.sort();
    alert(values);//0,1,10,15,5
    
很多情况下这种排序方式都不是最佳方案，因此sort()可以接收一个比较函数作为参数，以便指定哪个值位于哪个值前面。

    function compare(value1,value2){
        if(value1 < vlaue2){
            return -1;
        }else if(value1 > value2){
            return 1;
        }else {
            return 0;
        }
    }

    var values = [0,1,5,10,15];
    values.sort(compare);
    alert(values);//0,1,5,10,15
    
reverse()和 sort()方法的返回值是经过排序后的数组

对于数值类型或者其valueOf()方法会返回数值类型的对象类型，可以使用一个更简单的比较函数，这个函数只要用第二个值减第一个值即可。

    function compare(value1,value2){
        return value2 - value1;
    }

###针对数组元素的操作
**concat()和slice()不会改变原数组，splice()会改变原数组**
####concat()
先创建当前数组的一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新数组。

不传参时，他只是复制当前数组并返回副本

如果传递给concat()方法的是一个或多个数组，则将这些数组中的每一项都添加到结果数组中。

    var colors = ["red","green"];
    var colors2 = colors.concat("yellow",["black","brown"]);
    alert(colors);//red,green
    alert(colors2);//red,green,yellow,black,brown



####slice()
基于当前数组的一项或多个项创建一个新数组

接收一或两个参数，即要返回的项的起始和结束位置。

在只有一个参数的情况下，返回从该参数指定位置开始到数组末尾的所有项。

如果有两个参数，返回起始和结束位置之间的项，但不包括结束位置的项。

如果参数中有一个负数，则用数组长度加上该数来确定相应的位置。在一个包含5项的数组上调用slice(-2,-1)和调用slice(3,4)的结果是一样的。

    var colors = ["red","blue","green","black","yellow"];
    var colors2 = colors.slice(1,4);
    alert(colors);//red,blue,green,black
    alert(colors2);//blue,green,black

####splice()
返回一个数组，该数组包含从原始数组中删除的项。
#####删除
可以删除任意数量的项，只需指定两个参数，要删除的第一项的位置和要删除的项数。
#####插入
可以向指定位置插入任意数量的项，只需指定三个参数，起始位置、0（要删除的项数）和要插入的项
#####替换
可以向指定位置插入任意数量的项，并且同时删除任意数量的项，只需指定三个参数，起始位置、要删除的项数和要插入的任意数量的项。

第一个参数为负值，则加上数组长度，第二个参数为负数则不删除任何项。

var colors = ["red","blue","green"];
var removed = colors.splice(0,1);
alert(colors);//blue,green
alert(removed);//red

removed = colors.splice(1,0,"yellow","orange");//从位置开始插入两项
alert(colors);//blue,yellow,orange,green
alert(removed);//返回一个空数组

removed = colors.splice(1,1,"red","purple");//插入两项，删除一项
alert(colors);//blue,red,purple,orange,green
alert(removed);//yellow

#### 复制数组

把一个数组赋值给另一个数组时，只是为被赋值的数组增加了一个引用。

	var nums = [1,2,3];
    var nums2 = nums;
    nums[0] = 4;
    print(nums2[0]);//4
    
这种行为被称为浅复制，新数组依然指向原来的数组

要执行深复制，需将原数组中的每一个元素都复制一份到新数组中。

	function copy(arr,arr2){
    	for(var i=0; i<arr.length; i++){
        	arr2[i] = arr[i];
        }
    }

### 查找元素

以下两个方法都接收两个参数：要查找的项、表示查找起点位置的索引。比较第一个参数与数组中的每一项时，会使用全等操作符。

IE9以下浏览器不支持

#### indexOf()

用来查找传进来的参数在数组中是否存在，如存在返回该元素在数组中的索引，如不存在返回-1

#### lastIndexOf()

与indexOf类似，只是这个函数是从右往左查找

### 迭代方法

IE9以下IE浏览器不支持迭代方法

`map()`和`filter()`方法可以产生新数组

#### every()

接收一个返回值为布尔类型的函数，对数组中的每一项使用该函数

对数组中的每一项运行给定函数，如果该函数对每一项都返回true,则返回true

	function isEven(num){
    	return num % 2 == 0;
    }
    var nums = [2,4,6];
    var even = nums.every(isEven);//true  对数组中的每一项使用isEven函数都返回true
#### some()

接收一个返回值为布尔类型的函数，只要有一个元素使得该函数返回true，该方法就返回true

	var nums = [1,3,4];
    var even = nums.some(isEven);//true

#### forEach()

接收一个函数，对数组中的每个元素使用该函数

	function square(num){
    	print(num, num*num);
    }
    var nums = [1,2,3];
    nums.forEach(square);1 1   2 4   3 9
    
#### map()

对数组中每一个元素使用某个函数，返回一个新数组

	function sum(n){
    	return n += 1;
    }
    var nums = [1,2,3];
    var news = nums.map(sum);
    print(news);//[2,3,4]
    
#### filter()

传入一个返回值为布尔类型的函数，返回一个新数组，该数组包含应用该函数结果为true的元素

	var nums = [1,2,3];
    var news = nums.filter(isEven);
    print(news);//[2]
    
#### reduce()

接收一个函数，返回一个值。从一个累加值开始不断对累加值和数组中的后续元素调用该函数，返回得到的累加值

	function add(a,b){
    	return a + b ;
    }
	
    var nums = [1,2,3];
    var sum = nums.reduce(add);
    print(sum);//6
    
reduce()也可以用来将数组中的元素连接成一个长的字符串

`reduceRight()`是从右到左执行


