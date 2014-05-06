---
layout: post
title: 深度克隆
---
## 浅复制

引用类型按引用传递，传递的是内存中的地址。

    var person = {name:'me',age:12};
    var newperson = person;
    newperson.job = "doctor";
    console.log(newperson); 
    console.log(person);

复制person到newperson中，复制的是person在栈中的地址，所以这时person和newperson指向的是堆中的同一个对象，也就是说改变其中一个的属性值另一个的属性也会变。他们是相互影响的。这就是浅复制。

## 深复制

    function cloneObj(obj){
    
    	 if(typeof obj!='object'){
            return ;
        }
        
    
        var cloneobj = obj.constructor===Array?[]:{};
        
       
        for(var property in obj){
            if(obj.hasOwnProperty(property)){
            cloneobj[property]=typeof obj[property]==='object'?arguments.callee(obj[property]):obj[property];		}
        }
        return cloneobj;
    }

创建一个新对象，把obj中的属性复制到新对象中，新对象跟原对象指向不同的堆内容，相互间没有什么联系。
