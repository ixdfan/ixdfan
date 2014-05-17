---
layout: post
title: 正则引擎
---
POSIX NFA 和传统型NFA的主要差别

传统型NFA在遇到第一个完整匹配时就停止，POSIX NFA在给出结果之前必须尝试所有可能

如果没有完整匹配，传统型NFA也会尝试所有可能

### NFA与DFA

	用 to(nite|knight|night)
    
    匹配文本 at tonight

#### NFA的匹配过程：

正则表达式从t开始，每次查看表达式的一部分，同时检查当前文本是否匹配表达式的当前部分，如果不匹配，检查文本的下一个字符。

    //正则表达式中的t与文本中的a尝试匹配，匹配失败，t尝试匹配文本中的下一个字符
    
    -->to(nite|knight|night)
    -->at tonight

	//t尝试匹配文本中的t,匹配成功
    
    -->to(nite|knight|night)
    a-->t tonight

	//表达式中的o，尝试匹配文本中的空格，匹配失败
    
    t-->o(nite|knight|night)
    at--> tonight

	//移动文本的下一个字符空格，开始尝试匹配
    
    -->to(nite|knight|night)
    at--> tonight

	//匹配失败，移动到字符串下一个字符t,开始尝试匹配
    
    -->to(nite|knight|night)
    at -->tonight

	//匹配成功，表达式中的o尝试匹配文本的下一个字符o
    
    t-->o(nite|knight|night)
    at t-->onight

	//匹配成功，进入到表达式的多选结构，第一个分支的n尝试与文本中的n匹配
    
    to(-->nite|knight|night)
    at to-->night

	//匹配成功，重复上面的步骤
    
    to(n-->ite|knight|night)
    at ton-->ight
	
    //第一个分支中的t尝试与文本中的g匹配
    
    to(ni-->te|knight|night)
    at toni-->ght

	//匹配失败，尝试下一个分支的k,与文本中的n匹配
    
    to(nite|-->knight|night)
    at to-->night

	//匹配失败，尝试下一个分支的n,与文本中的n匹配
    
    to(nite|knight|-->night)
    at to-->night

	//重复上面的步骤，匹配成功
    
    to(nite|knight|n-->ight)
    at ton-->ight

####DFA的匹配过程

扫描字符串中的每个字符，对引擎进行控制。

    //扫描文本的第一个字符a，与正则的第一个字符t，不匹配

    -->at tonight
    -->to(nite|knight|night)

    //继续扫描文本的第二个字符t，与正则的第一个字符t匹配

    a-->t tonight
    -->to(nite|knight|night)

    //扫描文本的下一个字符空格，与正则的下一个字符o匹配，匹配失败

    at--> tonight
    t-->o(nite|knight|night)

    //扫描文本的下一个字符t，与正则的第一个字符匹配，匹配成功

    at -->tonight
    -->to(nite|knight|night)

    //扫描文本的下一个字符o，与正则的第二个字符匹配，匹配成功

    at t-->onight
    t-->o(nite|knight|night)

    //扫描文本的下一个字符n，与正则多选分支中每个分支的第一个字符匹配，匹配成功的继续匹配下一个字符，不成功的正则分支则舍去

    at to-->night
    to(-->nite|-->knight|-->night)

    at ton-->ight
    to(n-->ite|knight|n-->ight)

    at toni-->ght
    to(ni-->te|knight|ni-->ght)

    at tonig-->ht
    to(nite|knight|nig-->ht)

    //匹配成功
    at tonigh-->t
    to(nite|knight|nigh-->t)
