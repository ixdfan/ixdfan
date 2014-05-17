---
layout: post
title: 文档类型声明与怪异模式
category: html
---
< !DOCTYPE >声明不是HTML标签，它是指示web浏览器关于页面使用哪个HTML版本进行编写的指令。

## DTD

一个DTD文档包含元素的定义规则、元素间关系的定义规则、元素可使用的属性、可使用的实体或符号规则。

#### DTD的作用

* 验证器根据它来判断应采用何种验证规则来验证代码

* 保证HTML文档格式正确，可以通过比较HTML文档和DTD文件来看文档是否符合规范，以及元素和标签使用是否正确。

* 避免触发怪异模式

## 怪异模式

为了确保向后兼容，浏览器厂商发明了标准模式和怪异模式来解析网页。标准模式中浏览器根据规范来表现页面，怪异模式通常模拟老式浏览器的行为以防止老站点无法工作。

####激活怪异模式

* 未对文档类型进行定义

* 在文档类型定义之前出现非空格和换行字符，浏览器会激活怪异模式。

* 定义文档类型为激活怪异模式的类型


#### 怪异模式和标准模式的差异

* IE对盒模型的解析，怪异模式中IE使用IE盒模型，即width本身包含了padding和border的宽度。

* 经典的块居中方法（设定width，然后maigin:0 auto）无法正常工作。

##HTML5中的文档类型声明

<! DOCTYPE html>

在 HTML 4.01 中，< !DOCTYPE> 声明引用 DTD，因为 HTML 4.01 基于 SGML。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容。

HTML5 不基于 SGML，所以不需要引用 DTD。

####HTML5文档类型声明的好处

* 对于尚未支持HTML5的浏览器，它无法获得具体文档类型定义，默认激活标准模式，它会按照标准模式来解析文档

* 对于已经支持HTML5的浏览器，它会检测到这是HTML5的文档类型声明，激活相应解析模式，使HTML5特性可以表现出来

* 声明更简洁，不易出错。

##常用的文档类型声明
**HTML 5**
<!DOCTYPE html>

**HTML 4.01 Strict**

该 DTD 包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

**HTML 4.01 Transitional**

该 DTD 包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
"http://www.w3.org/TR/html4/loose.dtd">

**HTML 4.01 Frameset**

该 DTD 等同于 HTML 4.01 Transitional，但允许框架集内容。
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" 
"http://www.w3.org/TR/html4/frameset.dtd">

**XHTML 1.0 Strict**

该 DTD 包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。必须以格式正确的 XML 来编写标记。
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

**XHTML 1.0 Transitional**

该 DTD 包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。必须以格式正确的 XML 来编写标记。

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "
http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

**XHTML 1.0 Frameset**

该 DTD 等同于 XHTML 1.0 Transitional，但允许框架集内容。
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">

**XHTML 1.1**

该 DTD 等同于 XHTML 1.0 Strict，但允许添加模型（例如提供对东亚语系的 ruby 支持）。

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">



