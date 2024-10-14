---
title: '[Java Training]Week 1'
date: 2019-07-07 15:35:07
categories: Java
tags: Java
index_img: https://i.loli.net/2019/07/07/5d21cd23675da29020.jpg
---
# 0x00
    本系列-Java集训系列
    记录我带领小组进行Java学习，按照《Java核心技术》第十版进行学习
# 0x01
    废话不多说，开搞
## 第一章
    吧啦吧啦，一堆废话
    简单说下可以说的点吧，面向对象，使用了虚拟机来跨平台
    关于Java SE、Java EE、Java ME
    Java SE(Java Platform, Standard Edition):用于桌面或简单服务器应用的Java平台
    Java EE(Java Platform, Enterprise Edition):用于复杂服务器应用的Java平台
    Java ME(Java Platform, Micro Edition):用于手机和其他小型设备的Java平台
    简单理解就是，Java se是语言基础，里面包含了标准库，Java ee和Java me是在java se基础上进行的扩展，ee主要用于企业级开发，包括像java web开发，me主要是手机端，不过因为安卓，java me没有用武之地
    其他也没没了，都是自卖自夸的话
## 第二章
    搭建环境，首先是最基础的：
    运行java需要一个jre，包含了java的虚拟机jvm和一些标准库，可能还有其他一些乱七八糟的
    开发java需要一个jdk，主要包含了java的编译器
    值得一提的就是安装jdk的时候就已经带一个jre了，所以不用在额外装
[下载地址](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    如果链接失效就去网上找jdk下载
    我的环境是Windows的，安装就不详述了
    安装之后有一点需要说明下的就是环境变量，需要配一下环境变量
    [配置教程](https://www.runoob.com/w3cnote/windows10-java-setup.html)
    配置完之后就可以愉快的使用记事本开发了，不过我们都用IDE来进行开发
    主流选择是Eclipse与IDEA，IDEA更现代化，现在用的人比较多，Eclipse是以前很火，所以有不少老项目都是使用Eclipse开发的
    这里我先把eclipse的说下，以后在补IDEA的：
    [下载地址](https://www.eclipse.org/downloads/packages/)
    因为比较喜欢哪个经典图标，所以我下载的Eclipse IDE for Eclipse Committers
    ![eclipse下载](https://i.loli.net/2019/07/07/5d21c087838b425461.png)
    正常使用下载第一个就行
    如果是和我下载的一样的话，可以通过安装插件的方式来安装第一个里面的插件
    在eclipse的help->install new software
    ![进入安装插件界面](https://i.loli.net/2019/07/07/5d21c6714f47e17694.png)
    在work with 后面的框里输入http://download.eclipse.org/releases/2019-06
    ![显示插件](https://i.loli.net/2019/07/07/5d21c6714627b86652.png)
    注：最后面的2019-06是eclipse的版本号，在help->about eclipse ide
    ![查看版本号](https://i.loli.net/2019/07/07/5d21c6717bc3e56796.png)
    选择最下面的，ee以及其他插件，然后点击下一步下一步，中间有一个需要同意之后才能点下一步，之后就等安装完成，重启即可
    ![选择插件进行安装](https://i.loli.net/2019/07/07/5d21c67135f5845865.png)
