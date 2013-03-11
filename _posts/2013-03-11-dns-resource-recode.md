---
layout: post
title: "something about DNS resource recode"
description: ""
category: 
tags: []
---
{% include JB/setup %}
DNS中的条目成为资源记录(resource recode),比较重要的RR有A几率,AAAA记录,PTR,MX,CNAME等.

###A 记录
A记录把一个主机名映射成为一个32位的IPv4地址.


###AAAA 记录
四A记录,把一个主机名映射为一个128位的IPv6地址.四A代表位数是IPv4的四倍.

###PTR 记录
指针记录,PTR记录把IP地址映射为主机名.

###MX 记录
MX记录把一个主机指定作为给定主机的"邮件交换器".

###CNAME 记录
"canonical name"(规范名字),常见用法是为常用的服务指派CNAME记录,如果人们使用这些服务名而不是真是的主机名,那么相应的服务挪到另一个主机时他们也不必知道.例如,名为linux的主机有一下两个CNAME记录
    ftp   IN  CNAME  linux.unpbook.com
    http  IN  CNAME  linux.unpbook.com
