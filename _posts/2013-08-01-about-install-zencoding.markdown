---
author: admin
comments: true
date: 2013-08-01 07:59:48+00:00
layout: post

title: ' Dreamweaver装不上zen coding 和jqurey'

---




## 安装遇到问题





给dw装zen coding，刚开始是因为没有 adobe extension manager 打不开后缀名为.mxp的文件，这个简单，就在网上下了一个adobe extension manager cs5，这下好了，能打开.mxp了问题应该解决了，可是打开是能打开了，还是安不上zen coding，一打开就报错**“不能安装此拓展，需要8或更高版本的dreamweaver”**，试了n多次都不行，在网上找了各种方法都没有，什么删除menus里什么文件的，什么改文件里代码的，都以失败告终。

   看到网上有人说是dreamweaver版本的问题，我用的是绿色版，于是就在网上下dreamweavercs5、cs5.5、cs6的官方正式版，400多M的一个一个安装包以50多K/s的速度下下来后，居然安不上，下了一整天还安不上，当时那个烦人啊，一气之下把那些安装包全删了，还是安上原来的绿色版，继续在网上查zen coding安不上的解决方法。纠结了好几天，后来看到有人说，绿色版的只是保留了完整版最基本的功能所以安不上插件。
   
于是又花了一个小时左右下了一个完整版的dw，结果，安不上，总是报错“exit code 7”那个气人啊，就在网上找，找了好久试了好多种方法，说什么因为装了其他版本的dw建议下一个AdobeCreativeSuiteCleanerTool，好吧，下就下吧，清除了还是没用，又在开始里搜dreamweaver把搜到的相关文件都删了，再安装还是装不上。

无奈，又上网查，看有没有什么方法，看到有人说：“方法试了很多都安不上，**最好用的就是把c:\programdata\adobe删掉”，我删了再安装果然安上了，再安zen coding也安上了，又安jquery出了点问题，后来重新再网上下了一个版本的才装上。**

这个纠结了我好几天的问题终于解决了，真是大快人心啊。我就给大家说说具体的安装步骤吧，以免以后大家遇到相同的问题时能很快解决不要花那么多时间了。
关于dreamweaver 完整版装不上的问题


# **具体解决办法**




## ◆安装dreamweaver 完整版如果遇到下面的错误


**1.把电脑中已经安装的dreamweaver卸载，并删除相关文件，可在开始菜单搜一下“dreamweaver”把相关的以前版本的dreamweaver文件都删掉。**

**2.删掉c:\programdata\adobe文件**

**3**.如果进行步骤2还是安不上就删除c:\programfile\adobe文件



**◆关于zen coding 装不上的问题**

**“不能安装此拓展，需要8 或更高版本的dreamweaver”**

**如果你现在的dw是绿色版的，建议重安一个完整版的，绿色版只有基本功能安不上插件。**



◆更改**zen coding 快捷键**

1.zen coding以后重启dm

2.菜单栏里能看到zen coding，zen coding的第一个命令就是补全代码命令，它的快捷键默认是ctrl +。

3.你觉得不好用的话可以在编辑——快捷键——复制副本——选择zen coding——减去它现在的快捷键——在按键中按入新的快捷键（如果新的快捷键已经被用了，可以先找到用它的命令删去已用的快捷键，再给zen coding的快捷键改成这个）。



### ◆关于**jqurey安不上**的问题


**1.把shared、Extensions、codehints三个文件夹复制到一下路径即可**

WinXP:C:\Documents and Settings\Administrator\Application Data\Adobe\Dreamweaver CS5\zh_CN\Configuration

win7:C:\Users\Administrator\AppData\Roaming\Adobe\Dreamweaver CS5\zh_CN\Configuration

注意：Administrator可能需要替换为实际登陆账号所建的目录（AppData为隐藏文件夹）

**2.重新启动Dreamweaver CS5**

 （这个路径不一定跟你的一样，你只要把那三个文件夹复制到，你的dm的安装文件zh_CN\Configuration中就可以了。）






