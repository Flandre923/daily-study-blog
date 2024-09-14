---
title: 【Python 高级特性】装饰器：不修改代码，就能改变函数功能的强大特性
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/bdea021a-71e9-11ef-b238-ba1ea485754b.png
category: Python
draft: false
---


# 【Python 高级特性】装饰器：不修改代码，就能改变函数功能的强大特性

[【Python 高级特性】装饰器：不修改代码，就能改变函数功能的强大特性_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Uz421Z79L/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

一个一般的function

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c1c533f2-71e9-11ef-92fd-ba1ea485754b.png)​

定义装饰器wrapper

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c2acf8a1-71e9-11ef-867c-ba1ea485754b.png)​

去调用一个装饰器

​![image]()​

一种更加简单的语法

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/01eadb56-71ea-11ef-bf35-ba1ea485754b.png)​

如何定义一个装饰器的生成器

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/02d8357c-71ea-11ef-a92f-ba1ea485754b.png)​

调用

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/03b43287-71ea-11ef-9e4e-ba1ea485754b.png)​

存在问题

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/050f2941-71ea-11ef-ae8a-ba1ea485754b.png)如果此时打印装饰后的函数的名称，那么这个函数名称就会变为函数的名称。

‍

修复这个问题

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/05b2c696-71ea-11ef-98bb-ba1ea485754b.png)​

使用一下自带的一个工具。他也是一个装饰器。

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
