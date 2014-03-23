---
layout: post
title: 字符串相关的方法
---
## 转换为字符串

###toString()

返回相应值的字符串

null和undefined值没有这个方法

多数情况下，toString方法不必传参。调用数值的toString方法时，可以传递一个参数即输出数值的基数，输出任意有效进制格式表示的字符串。

    var num = 10;
    alert(num.toString(2));//"1010"

### string()

将任何类型的值转换为字符串

string函遵循下列转换规则：

* 如果值有toString方法，则调用该方法并返回相应的结果

* 如果值是null，则返回“null”

* 如果值是undefined，则返回“undefined”

###fromCharCode()
接收一或多个字符编码，然后把它们转换成一个字符串

	alert(String.fromCharCode(104,101,108,108,111));//hello
##访问字符串中特定字符

### charAt()

接收一个参数——基于0的字符位置

以单字符字符串的形式返回给定位置的那个字符

    var stringValue = "hello world";
    alert(stringValue.charAt(1));//"e"

### charCodeAt()

接收一个参数——基于0的字符位置

输出给定位置字符的字符编码

    alert(stringValue.charCodeAt(1));//101

## 字符串操作方法
### concat()
将一个或多个字符串拼接起来，返回拼接得到的新字符串。

    var stringValue = "hello ";
    var result = stringValue.concat("world","!");//可接受任意多个参数
    alert(stringValue);//"hello"
    alert(result);//"hello world!"

**在实际中更多的是用加法操作符来拼接字符串，更简单易行。**

### slice() substr() substring()

接收一个或两个参数，返回被操作字符串的一个子字符串，对原始字符串没有任何影响。

第一个参数指定字符串开始的位置，如果没有第二个参数将字符串长度作为结束位置

slice()和substring()第二个参数表示字符串的结束位置，但不包含该位置的字符

substr()的第二个参数指定返回字符的个数。

如果传入的参数是负值，slice()会将传入的负值与字符串长度相加；substr()将负的第一个参数与字符串长度相加，将负的第二个参数转换为0；substring()将所有负值参数都转换为0。

IE中向substr()传递负值时，它回返回原始的字符串

    var stringValue = "hello world";
    
    alert(stringValue.slice(3));//"lo world"
    alert(stringValue.substring(3));"lo world"
    alert(stringValue.substr(3));//"lo world"
    alert(stringValue.slice(3,7));//"lo w"
    alert(stringValue.substring(3,7));"lo w"
    alert(stringValue.substr(3,7));"lo worl"

##从字符串中查找子字符串
###indexOf() 和lastIndexOf()
从一个字符串中搜索给定的子字符串，然后返回子字符串的位置，如果没有找到该子字符串就返回-1

indexOf()从字符串的开头向后搜索子字符串

lastIndexOf() 从字符串的末尾向前搜索子字符串

第一个参数表示要搜索的子字符串，第二个参数表示从字符串中的哪个位置开始搜索。

    var stringValue = "hello world";
    
    alert(stringValue.indexOf("o",6));//7
    alert(stringValue.latIndexOf("o",6));//4

**可以通过循环调用indexOf()或lastIndexOf()来找到所有匹配的子字符串**

    var stringValue = "Lorem ipsum dolor sit amet,consectetur adipisicing elit";
    var positions = new Array();
    var pos = stringValue.indexOf("e");

    while(pos > -1){
        positions.push(pos);
        pos = stringValue.indexOf("e",pos+1);
    }

    alert(positions);//3,24,32,35,52
    
##字符串大小写转换
### toLowerCase() 和 toUpperCase()
不针对地区的实现
### toLocalLowerCase() 和 toLocalUpperCase()
针对特定地区的实现

对有些地区来说，针对地区的方法与其通用方法得到的结果相同，但少数语言会为Unicode大小写转换应用特殊的规则，这时候就必须使用针对地区的方法来保证实现正确的转换。

在不知道自己的代码将在哪种语言环境中运行的情况下，最好使用针对地区的方法。

##字符串的模式匹配方法
###match()
只接受一个参数，要么是一个正则表达式要么是一个RegExp对象

返回一个数组，第一项是与整个模式匹配的字符串，之后的每一项保存着与正则表达式中捕获组匹配的字符串。没有匹配项返回null

    var text = "cat,bat,sat,fat";
    var pattern = /.(at)/;

    var matches = text.match(pattern);

    alert(matches.length);//2
    alert(matches[0]);//"cat"
    alert(matches[1]);//"at"
    
### search()
只接受一个参数——由字符串或RegExp对象指定的一个正则表达式

返回字符串第一个匹配项的索引，没有找到则返回-1

始终从字符串开头向后查找

    var text = "cat,bat";
    var pattern = /at/;

    var result = text.search(pattern);
    alert(result);//1即"at"在字符串中第一次出现的位置

### replace()
替换子字符串

接收两个参数，第一个参数可以是一个RegExp对象或一个字符串，第二个参数可以是一个字符串或函数。

####如果第一个参数是字符串
那么只会替换第一个子字符串。要替换所有子字符串就要提供一个正则表达式而且指定全局。

####如果第二个参数是字符串
可以使用一些特殊字符序列，将正则表达式操作得到的值插入到结果字符串中。

    var text = "cat,bat,sat,pat";

    var result = text.replace("cat","ond");
    alert(result);//cond,bat,sat,pat

    result = text.replace(/at/g,"ond");
    alert(result);//cond,bond,sond,pond

    result = text.replace(/(.at)/g,"word($1)");
    alert(result);//word(cat),word(bat),word(sat),word(pat)

####如果第二个参数是函数
在只有一个匹配项的情况下，会向这个函数传递三个参数：模式的匹配项、模式匹配项在字符串中的位置和原始字符串

在正则表达式定义了多个捕获组的情况下，传递给函数的参数依次是：模式的匹配项、第一个捕获组的匹配项、第二个捕获组的匹配项.....，最后两个参数仍然是模式的匹配项在字符串中的位置和原始字符串。

这个函数返回一个字符串，表示应该被替换的匹配项。

    function htmlEscape(text){
        return text.replace(/[<>"&]/g,function(match,pos,originalText){
                switch(match){
                    case "<":return "&lt;";
                    case ">":return "&gt;";
                    case "&":return "&amp;";
                    case "\"":return "&quot;";
                }
        });
    }
    alert(htmlEscape("<p class=\"greeting\">"</p>));//&lt;p class=&quot;greeting&quot;&gt;&lt;/p&gt;


####特殊字符序列
* $$ 匹配$

*  $& 匹配整个模式的子字符串

*  $' 匹配子字符串之前的字符串

*  $` 匹配字符串之后的字符串

*  $n 匹配第n捕获组的子字符串
* $nn 匹配第nn个捕获组的子字符串

### split()
基于指定的分隔符将一个字符串分割成多个子字符串，并将结果放在一个数组中。

第一个参数是分隔符，分隔符可以是字符串，也可以是一个RegExp对象

第二个参数用于指定数组的大小

    var colorText = "red,blue,green,yellow";
    var colors1 = colorText.split(",");
    alert(colors1);//"red","blue","green","yellow"

    var colors2 = colorText.split(",",3);
    alert(colors2);//"red","blue","green"

    var colors3 = colorText.split(/[^\,]+/);
    alert(colors3);//第一项和最后一项是空字符串，因为正则表达式指定的分隔符出现在了字符串的开头和末尾。"",",",",",",",""


##比较两个字符串
###localeCompare()

如果字符串在字母表中应该排在字符串参数之前，则返回一个负数。具体的值要视实现而定。

如果字符串等于字符串参数，则返回0

如果字符串在字母表中应该排在字符串参数之后，则返回一个正数。具体的值要视实现而定。

因为localeCompare返回的值要视实现而定，所以最好像下面例子所示的这样使用这个方法：

    function determinOrder(value){
        var result = stringValue.localeCompare(value);
        if(result<0){
            alert("The string 'yellow' comes before the string '"+value+"'.");
        }else if(result>0){
            alert("The string 'yellow' comes after the string '"+value+"'");
        }else{

            alert("The string 'yellow' is equal to the string '"+value+"'.");
        }


    }
	var stringValue = "yellow";
    
    determinOrder("brick");
    determinOrder("yellow");
    determinOrder("zoo");

这种结构就可以确保代码在任何实现中都可以正确运行。


