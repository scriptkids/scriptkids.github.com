---
layout: post
title: "Unix Network Programming"
description: ""
category: 
tags: []
---
{% include JB/setup %}
这是一篇笔记性质的文章,记录以下怎么编译<UNIX Network Programming>卷一上面的样例代码.

首先在网上下载unpv13e,解压缩之后,进入目录执行:
    $./configure
    $cd lib
    $make 
这样会在lib上层目录中生成libunp.a
这样,复制config.h 和libunp.a到工作目录(就是写代码的目录)
接下来就可以工作目录中写代码拉..
编译的时候只需要加上参数就可以拉.. 例如:
    $ gcc -o client client.c -L ./ -lunp
到此,搞定收工...
