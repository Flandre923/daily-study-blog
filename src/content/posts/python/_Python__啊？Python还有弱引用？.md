---
title: ' Python  啊？Python还有弱引用？'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/6556535505678c8e58c6f84264ceaa5d820d625e55ffbcf7dab9a39bd19eb3d9.jpg
category: Python
draft: false
---


# [Python] 啊？Python还有弱引用？

# [[Python] 啊？Python还有弱引用？](https://www.bilibili.com/video/BV1ev8Je1EH5/?spm_id_from=333.788&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

强引用是指一般的引用，例如![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0a575f34f47d3a31246638a93f24ed26f5395896954c5faf14a75f4bbb50bc04.png)，这里的u1，u2就是强引用，强引用只要还存在着引用，这个内存就不会被GC回收。

弱引用就是和强引用相对应的，只要这个实例没有强引用，那么这个弱引用就会被回收，并且存在的数据结构也会被删除。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/9e177fa788039272dbe2f95cde8adfb008d8b239dea9aea4dd71e5fae374d4a1.png)导入包

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/be34fa54b5b36597a1fe5830bdff08117544fdf0b74048ed17d2d28d0aadb800.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/5f8ae8a3d9afcf257a47985efb7fa701de8e86e9763e6f1d36f683a0d7244acd.png)当chat room被方法运行结束之后，那么对应的user的强引用就没有了，那么自然对应的字典的是弱引用的， 那么就会被gc回收。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/eeb52aad3ec64f0eeba6e3a4fcae8097d1bf38241b991a5b6bde9db404d9acaa.png)​

‍

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/68ed58f771ad1d5e7b6a9ae7f804fa559150672b6f2e0e78ef78d67ca6251b01.png)python提供的弱引用

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3ace77483f575fe54f4dd22d24ed89a408a516a08b769dcdc9329500f6d1dbf7.png)单独创建弱引用

‍

数字，字符串等不支持弱引用

‍

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
