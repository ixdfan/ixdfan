---
author: admin
comments: true
date: 2014-02-08 09:38:01+00:00
layout: post

title: JavaScript中的表单

---

**表单事件处理函数**
1.onClick，是submit或button输入类型的一个属性，接受或拒绝提交
2.onSubmit,form标签的属性，用来控制用户单击提交按钮后的处理,单击提交按钮或回车时触发。
3.onReset,form的属性，用来 接受或拒绝重置操作



**表单方法**



      <a href="#" onClick="JavaScript: myForm.submit();"></a>
         //submit(),会像用户单击了提交按钮一样提交myForm表单
         
     <a href="#" onClick="JavaScript: myForm.reset();"></a>
        //reset(),将myForm表单中的值重置为默认值


通过这两个方法，可以在表单被发送到服务器之前，要求用户进行确认、检查输入等。

表单中的每个元素都有一个form属性，表示该元素所在表单的引用


    <form action="" name="myForm">
        <input onclick="return checkForm(this.form)" type="text" value="" />
    </form>


this表示当前对象input，this.form表示input所在的表单myForm


**在弹出窗口中显示表单的内容**
1.window.open()打开一个新窗口
2.获取用户输入到表单中的数据
3.在新窗口中打印出获取到的数据

选择列表select js可给select命名但不能给其选项命名。select有一个options属性，这个属性是所有选项元素的数组，我们可以用options数组来访问、移除或添加选项。selectedIndex属性表示已被选中的选项的索引数，如没有任何选项被选中，则为-1。
