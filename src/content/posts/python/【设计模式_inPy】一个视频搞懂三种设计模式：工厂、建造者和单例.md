---
title: '【设计模式 inPy】一个视频搞懂三种设计模式：工厂、建造者和单例'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/accd84c63856d6807cfb958d7e6f9f85259e5b5528f2f0a6399cf1af09e6ad45.jpg
category: Python
draft: false
---


# 【设计模式 inPy】一个视频搞懂三种设计模式：工厂、建造者和单例

[【设计模式 inPy】一个视频搞懂三种设计模式：工厂、建造者和单例_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV131421876N/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/6eaa6437964f168f8457ce5a8d9210c967fb4008ea88f30b1d2a7e9029c50368.png)存在的问题是，这个数据库的连接参数存在多个位置的，如果出问题修改是需要再多个位置修改的， 并且代码存在重复。

‍

更改为工厂模式

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/38d936fc3d12964c99a4b334c6a99a9124c0390cf900b6be5c309e22dacc70ae.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/9286246e20e950a865702154f45daca1a08dda6c7223f4e884bc131c8080a093.png) client改写

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/ea8a039073a41cafedec80d71420cd3260cd830180b8940233f260136fc22ab3.png)创建一个配置文件，将内容放置到配置文件中。

‍

‍

# 建造者模式

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/ba14477683418ede37a6b22d596482e55b99d155f199e11fe8cec45a16227b4e.png)​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0917061fb48704a075eeb9d8cad738b41411e50f615f1631a6211ff414049370.png)像这种要传入大量的参数的类，可以使用builder方法。

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f582e0826eef8d135d01914a15263fc5eeb8a129b1ed38afc65179099cf64777.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/4e314c1ae355eff2d04f83ef4b3f28258e799f752b05f9940523bf04192f3168.png)再build中创建实例。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/65b01e06f2635fbb10896976250bd134c32e19a68a1cc43c8852538a1f04ede9.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/53c7de278b22c43746d5e8dec357859deae592097ee324fd171ab9445ac6d910.png)调用

‍

# 单例

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/bf3753d8c2167131c905d5b1dd295f012a0e8f8a21b0504bb44e3e5e78ffe0cb.png)new 方法是object的方法， 是创建类的方法，然后new回去调用init，一般情况下是不需要去重写new的。参数中的cls表示当前的类。

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
