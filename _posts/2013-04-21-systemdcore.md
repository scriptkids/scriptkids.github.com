---
layout: post
title: "systemd下调试core文件"
description: ""
category: 
tags: []
---
{% include JB/setup %}
  最近在写代码的时候发现archlinux自从全面转到systemd下之后就不在当前目录生成core文件了，查了一下发现现在改成这种方式：
  需要手动执行 sudo sytemd-coredumpctl list 来查看系统中的出core程序以及core文件，使用sudo systemd-coredumpctl dump -o filename命令，会生成最后一次出core程序的core文件，也可以通过指定程序名或者PID的方式来生成指定程序的core文件。
  之后就依照原来的方式 gdb program core来调试程序啦～
