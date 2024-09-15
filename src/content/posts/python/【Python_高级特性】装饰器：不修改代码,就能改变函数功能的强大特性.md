---
title: '【Python 高级特性】装饰器：不修改代码,就能改变函数功能的强大特性'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f30f837269c5fd6694875445b6dec35f1112696cc7c1d17f787766f17a512938.jpg
category: Python
draft: false
---


# 【Python 高级特性】装饰器：不修改代码，就能改变函数功能的强大特性

[【Python 高级特性】装饰器：不修改代码，就能改变函数功能的强大特性_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Uz421Z79L/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

一个一般的function

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c3cad90826998e092921d65d1693014d1963937e7fdc9a9562122e1d607a37a0.png)​

定义装饰器wrapper

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/6e188b5519cd48f43d43544336ac51779d50eccb0cfd7b3f6015e483f7d71f59.png)​

去调用一个装饰器

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/8fd1575c947a9bf2f18fd27ad59cec22900370ad5c850e5af12beb0a2dde36f5.png)​

一种更加简单的语法

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/4a2b6369792625791a2cb7d0d69e57e25d9ecee6bc5ecdcf4f1aa910d1497347.png)​

如何定义一个装饰器的生成器

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c179f77b7953afa60a0d31b7bb6f5ddb11f424432f72dafba33719ad9c37cd0b.png)​

调用

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/350e4f45f02d08e137c978f8f31956109db93e87eb5012f2c5090a18522bddf3.png)​

存在问题

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/cad07f7b81dd42ca0ff8aa3de793013268a7e9305d9b8aa0fdc0ea77e733ba1c.png)如果此时打印装饰后的函数的名称，那么这个函数名称就会变为函数的名称。

‍

修复这个问题

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/ec8a161cd889ab8391326171f85abf1a53ba5c224d6ef507e3e4e9f473e8f7b7.png)​

使用一下自带的一个工具。他也是一个装饰器。

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
