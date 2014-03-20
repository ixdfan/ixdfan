---
layout: post
title: 引用类型之三 Date

---
    var now = new Date();//当前时间
    var now = new Date(May 25,2014);
    var now = new Date(2000,0);
    
在调用构造函数Date而不传参数的情况下，新创建的对象自动获得当前日期和时间。如果想根据特定的日期和时间创建日期对象，必须传入表示该日期的毫秒数。

如果将表示日期的字符串传给Date构造函数，会在后台调用Date.parse()或者Date.UTC()方法

## Date.parse() 和Date.UTC()
### Date.parse()
Date.parse()方法接受一个表示日期的字符串参数，然后返回这个字符串相应日期的毫秒数。

如果传入的字符串不能表示日期，则返回NaN

因为ECMA-262没有定义Date.parse()应该支持哪种格式，这个方法的行为会因实现而异，而且通常是因地区而异。将地区设置为美国的浏览器通常都接受下列日期格式：

* “月/日/年” 如 1/3/2014
* 英文月名 日，年 如 January 12,2014
* 英文星期几 英文月名 日 年 时：分：秒 时区 如 Tue May 25 2014 00:00:00 GMT-0700

### Date.UTC()

Date.UTC()也返回表示日期的毫秒数

参数分别是：年、基于0的月份、日、时、分、秒以及毫秒数

这些参数中只有年和月是必须的，如果没有提供日则假设为1，省略其他参数则假设为0

日期和时间都是基于本地时区而非GMT来创建的。

##继承的方法
与其他引用类型一样，Date类型也重写了toLocalString()、toString()和valueOf()方法。
### toLocalString()
toLocalString()会按照与浏览器设置的地区相适应的格式返回日期和时间，意味着时间格式中会包含AM或PM，但不会包含时区信息。
### toString()
toString()通常返回带有时区信息的日期和时间，其中时间一般用军用时间表示（小时的范围是0-23）
### valueOf()
valueOf()返回日期的毫秒表示，可以使用比较操作符来比较日期值。

##日期格式化方法

* toDateString()——以特定实现的格式显示星期几、月、日、年

* toTimeString()——以特定实现的格式显示时、分、秒和时区

* toLocalTimeSting()——以特定地区的格式显示时、分、秒

* toLocalDateString()——以特定于地区的格式显示星期几、月、日、年

* toUTCString()——以特定于实现的格式显示完整的UTC日期

## 日期/时间组件方法
直接取得或设置日期中特定部分的方法

UTC日期指的是在没有时区偏差的情况下（将日期转换为GMT时间）的日期值。

* getTime()——返回表示日期的毫秒数，与valueOf()方法返回的值相同

* setTime()——以毫秒数设置日期，会改变整个日期

* getFullYear()——取得四位数的年份

* getUTcFullYear()——返回UTC日期的4位数年份

* setFullYear()——设置日期的年份，传入的年份值必须是4位数字

* setUTCFullYear()——设置UTC日期的年份，传入的年份值必须是4为数字

* getMonth()——返回日期中的月份，其中0表示1月

* getUTCMonth()——返回UTC日期中的月份，其中0表示1月

* setMonth()——设置日期的月份，传入的月份值必须大于0，超过11则增加年份

* setUTCMonth()——设置UTC日期的月份，传入的月份至必须大于0，超过11则增加年份

* getDate()——返回日期中的日

* getUtcDate()——返回UTC日期中的日

* setDate()——设置日期中的日

* setUTCDate()——设置UTC日期中的日

* getDay()——返回日期中的星期几，其中0表示星期日

* getUTCDay()——返回UTC日期中的星期几，其中0表示星期日

* getHours()——返回日期中的时（0-23）

* getUTCHours()——返回UTC日期中的时（0-23）

* setHours()——设置日期中的小时数，传入的值超过了23则增加天数

* setUTCHours()——设置UTC日期中的小时数，传入的值超过了23则增加天数

* getMinutes()——返回日期中的分钟数 （0-59）

* getTUcMinutes()——返回UTC日期中的分钟数（0-59）

* setMinutes()——设置日期中的分钟数，传入的数超过59则增加小时数

* setUTCMinutes()——设置UTC日期中的分钟数，传入的数超过59则增加小时数

* getSeconds()——返回日期中的秒（0-59）

* getUTCSeconds()——返回UTC日期中的秒（0-59）

* setSeconds()——设置日期中的秒，传入的值超过59则增加分钟数

* setUTCSeconds()——设置UTC日期中的秒，传入的值超过59则增加分钟数

* getMilliseconds()——返回日期中的毫秒数

* getUTCMilliseconds()——返回UTC日期中的毫秒数

* setMilliseconds()——设置日期中的毫秒数

* setUTCMilliseconds()——设置UTC日期中的毫秒数

* getTimezoneOffset()——返回本地时间与UTC时间相差的分钟数。