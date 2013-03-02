---
layout: post
title: "Linux下静态库与动态库"
description: ""
category: 
tags: []
---
{% include JB/setup %}
参考链接:[1](http://www.cnblogs.com/feisky/archive/2010/03/09/1681996.html)
##静态库和动态库的区别
1.静态函数库
  这类库的名字一般是libxxx.a;利用静态函数库编译成的文件比较大,因为整个函数库的所有数据都会被整合进目标代码中.有点是编译后执行程序不需要外部的函数库支持,因为所有使用的函数都被编译进去了.缺点是,函数库变化了,程序必须重新编译.

2.动态函数库
  这类库的名字一般是libxxx.so;相对于静态函数库,动态函数库在编译的时候,并没有被编译进目标代码中,只有在执行的时候才调用函数库里的函数,因此产生的可执行文件比较小.

##静态库的使用举例
1.静态库代码pr1.c pr2.c
    $cat pr1.c
    void print1()
    {
        puts("this is the first lib src!");
    }
    $cat pr2.c
    void print2()
    {
        puts("this is the second lib src!");
    }
2.编译.c文件
    $gcc -c pr1.c pr2.c   //-c参数不进行链接
3.链接静态库 静态库名字必须是lib[name].a的规则
    $ar -rsv libpr.a pr1.o pr2.o
4.调用库函数代码
    $cat main.c
    int main()
    {
        print1();
        print2();
    }
5.编译链接选项
  -L及0l参数放后面,-L加载库文件路径,-l指明库文件名字
    $gcc -o main main.c -L ./ -lpr

##动态库的使用
1.设计动态库代码
    $cat pr3.c
    int p=2;
    void print()
    {
        puts("this is the first dll src!");
    }
2.生成动态库
    $gcc -fpic -shared -o dl.so pr3.c
##动态库的隐式调用
    $cat main.c
    int main()
    {
        print();
    }
编译指明动态库名字位置
    $gcc -o tdl main.c ./dl.so
###动态库的显式调用
动态函数库的显式调用主要需要四个函数
+dlopen 打开动态库
+dlsym  获取动态库中对象基址
+dlerror 获取显式动态库操作中的错误信息
+doclose 关闭动态库

    $cat main3.c
    #include <dlfcn.h>
    int main(void)
    {
        void *pHandle;
        void (*pFunc()); //指向函数的指针
        int *p;
        pHandle = dlopen("./dl.so",RTLD_NOW); //打开动态库
        if(!pHandle){
            puts("can't find dl.so");
            exit(1);
        }
        pFunc=(void (*)())dlsym(pHandle,"print");
        if(pFunc)
            pFunc();
        else
            puts("can't find function print");
        p = (int *)dlsym(pHandle,"p");
        if(p)
            printf("p=%d\n",*p);
        else
            printf("Can;t find int p\n");
        dlclose(Phandle);
        return 0;
        }

        $gcc -o tds main3.c -ldl -L .
        
        
##库依赖的查看
使用ldd命令来查看执行文件依赖于那些库
    $ldd [-vdr] filename 
