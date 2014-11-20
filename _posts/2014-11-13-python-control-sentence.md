---
layout: post
title: python控制语句和多重赋值
category: Python
---
## 多重赋值

	aInt,bInt,cInt = 1,23,3

上面的语句相当于：

	aInt = 1
    bInt = 23
    cInt = 3
    
执行多重赋值时，要确保变量和值的个数相等，否则会报错

### 交换两个变量的值

	aInt = 1
    bInt = 23
    aInt,bInt = bInt,aInt
    
通过多重赋值，可以非常方便的交换两个变量的值

实际是通过把值存储在临时存储单元中，两个临时变量来进行交换

## 控制语句

### 1.if elif else
### 2.for in
### 3.while

#### else 和 break

在while循环结束时，可以使用else从句

	while booleanExpression:
    	#suite1
        break
    else:
    	#suite2

当while循环布尔表达式为假时，进入else子句。初始表达式为假，while循环一次都不执行，直接执行else语句。

`break`语句用于退出执行循环，并跳过循环体中其余部分，包括else代码块

#### continue

	numStr = raw_input("Number:")
    theSum = 0
    while numStr != '.':
    	if not numStr.isdigit():
        	print 'Error,only number please'
            numStr = raw_input('Number:')
            continue
        theSum += int(numStr)
        numStr = raw_input('Number:')
    print theSum

continue结束本次循环，继续下一次循环