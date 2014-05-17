---
layout: post
title: 表单中的type=hidden
category: js
---
< input type="hidden"/>定义隐藏字段。隐藏字段对于用户是不可见的。隐藏字段通常会存储一个默认值，它们的值也可以由JS进行修改。

    <form >
        <input type="text" name="username">
        <input type="hidden" name="country" value="Norway">
    </form>

当用户提交这个表单时，就会有两个名值对发送到服务器端，username=&country=Norway

**注意：**

* 这种输入类型用户无法控制，但是却在提交表单时发送value属性的值

* 该元素通常用来传输一些客户端到服务器的状态信息。最好不要用此元素来传递敏感信息，因为用户可以通过查看源代码看到该元素属性的值。
