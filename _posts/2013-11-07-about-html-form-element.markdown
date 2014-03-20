---
author: admin
comments: true
date: 2013-11-07 01:15:07+00:00
layout: post

title: 表单元素及相关属性

---



表单的作用：把信息传递给服务器

**< form>< /form>**创建个表单，用于包含其他表单元素

表单元素必须放入form中才有作用

    <form  action="form_action.asp"  method="post"  name="表单名称">

Action=url(地址)规定传递表单时，向何处发送表单数据

Method="post"数据处理方法，默认值是get。post可传递大量信息；get适合传递少量信息，会把值附在网页链接的后面

##input

**Input**标记必须有type和name属性，name属性便于服务器识别

    <input  value="初始值"  type="表单类型"  name="表单名称"  size="3"  maxlength="6"  readonly="readonly"  disabled="disabled" />

最多输入6个字符，最多显示3个字符。Readonly只和type=”text“配合使用，可选中显示闪烁光标，但是不能更改；disabled不能选中，相当于处于灰色状态

 Type=text普通文本

*   Password密码

*   Radio 单选按钮

*   Reset 重置按钮

*  Submit 提交按钮

*   Button 普通按钮

*   Checkbox 复选框

*   File 浏览框

*  Image 图片按钮

*  Hidden 隐藏域


##lable

**<lable>**标注的内容</lable>为input元素定义标注

    <lable  for="man" >男</lable>

    <input  type="radio"  name="sex"  value="男"  id="man">

当for的属性值和id的属性值相同时，标签和按钮相关，点标签“男”就可选中单选按钮


##select
    <**select** name=""  size="显示的行数"  multiple="multiple"（可多选）>

     <option  selected="selected"  value=“提交值“（如果没有提交值，浏览器读不到option标签中的内容）>

    <optgroup  label="分组名称">

    <option></option>

    <option></option>

    </optgroup>

    </select>


##textarea
    <textarea name=""  cols="每行中的字符数"  rows="多少行">

##fieldset

    <form>

    <fieldset>

    <legend>围绕表单元素边框的标题</legend>

       其他表单元素

    </fieldset>

    </form>

Fieldset没有宽度属性，默认占满整个父级的宽度










