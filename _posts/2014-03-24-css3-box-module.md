---
layout: post
title: CSS3.0 盒模型
category: css
---
## 父容器的box
父容器里面的box属性包括哪些box属性，具体属性如下代码所示：
box-orient | box-direction | box-align | box-pack | box-lines

### box-orient

box-orient(orient译为排列更准确)用来确定父容器里子容器的排列方式，是水平还是垂直。可选属性如下所示：horizontal | vertical | inline-axis | block-axis | inherit
horizontal、inline-axis


如果父容器选择horizontal或inline-axis属性对子容器进行水平排列，其是对父容器的宽度进行分配划分。此时如果父容器定义了高度值，其子容器的高度值设置则无效状态，所有子容器的高度等于父容器的高度值；如果父容器不设置高度值，其子容器的高度值才有效并且取最大高度值的子容器的高度。

如果父容器选择vertical或block-axis属性对子容器进行垂直排列，其是对父容器的高度进行分配划分。此时如果父容器定义了宽度值，其子容器的宽度值设置则无效状态；如果父容器不设置宽度值，其子容器的宽度值才有效并且取最大宽度值的子容器的宽度。

### box-direction

box-direction用来确定父容器里的子容器排列顺序，具体属性如下：normal | reverse | inherit

normal是默认值,按照HTML文档里结构的先后顺序依次展示。

reverse表示反转

### box-align

box-align表示父容器里面子容器的垂直对齐方式，可选参数如下所示：start | end | center | baseline | stretch

start在box-align表示居顶对齐

end表示居底对齐

center表示居中对齐

stretch 表示拉伸，拉伸到父容器等高

### box-pack
表示父容器里子容器的水平对齐方式

可选参数：start | end | center |justify

start 表示水平居左对齐

end 表示水平居右对齐

center 表示水平居中对齐

justify 表示水平等分父容器宽度






## box-flex 属性

box-flex主要让子容器针对父容器的宽度按一定规则进行划分

目前box-flex属性还没有得到firefox、Opera、chrome浏览器的完全支持，但可以使用它们的私有属性定义firefox(-
moz)、opera(-0)、chrome/safari（-webkit)。


### 按比例划分

    .wrap{
        width:600px;
        height:200px;
        display:-moz-box;
        display:-webkit-box;
        display:box;
        //必须给父容器wrap定义css属性display:box其子容器才可以进行划分(如果定了display:box则该容器则定义为了内联元素，使用margin:0px auto让其居中是无效的，要想使其居中只能通过它的父容器的text-align:center);
    }
    
    
    .sectionOne{
        background:orange;
        -moz-box-flex:3;
        -webkit-box-flex:3;
        box-flex:3;
    }
    .sectionTwo{
        background:purple;
        -moz-box-flex:2;
        -webkit-box-flex:2;
        box-flex:2;
    }
    .sectionThree{
        -moz-box-flex:1;
        -webkit-box-flex:1;
        box-flex:1;
        background:green;
    }

 


分别给sectionOne、sectionTwo、sectionThree的box-flex设置了3、2、1，也就是说这三个子容器将父容器wrap的宽度600px分为6份，sectionOne占居父结构宽度的3/6即300px，sectionOne占居父结构宽度的2/6即200px，sectionThree占父结构宽度的1/6即100px。

### 子容器设置了固定宽带

子容器如果设置了固定宽度值，该子容器则直接应用设置的宽度值，其它没有设置的则再父容器的宽度基础上减去子容器设置的固定宽度，在剩下的宽度基础上按一定比例进行划分分配。

    .wrap{
        width:600px;
        height:200px;
        display:-moz-box;
        display:-webkit-box;
        display:box;
    }
    .sectionOne{
        background:orange;
        -moz-box-flex:3;
        -webkit-box-flex:3;
        box-flex:3;
    }
    .sectionTwo{
        background:purple;
        -moz-box-flex:1;
        -webkit-box-flex:1;
        box-flex:1;
    }
    .sectionThree{
        width:200px;//设置固定宽度
        background:green;
    }

sectionThree设置了固定宽度为200px，父容器的宽度600px-200px，剩下的400px按box-flex设置的值进行划分，sectionOne占3/4即300px,sectionTwo占1/4即100px;

### 子容器添加了外边距

如果给子容器添加了外边距，则父容器的宽度减去子容器的外边距，再按box-flex设置的值进行分配。
