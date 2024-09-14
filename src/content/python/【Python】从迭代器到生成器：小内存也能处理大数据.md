---
title: 【Python】从迭代器到生成器：小内存也能处理大数据
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/20a17abe-71ea-11ef-9ac6-ba1ea485754b.jpg
category: Python
draft: false
---


# 【Python】从迭代器到生成器：小内存也能处理大数据

[【Python】从迭代器到生成器：小内存也能处理大数据_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1jt421c7yN/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/223855ee-71ea-11ef-a1af-ba1ea485754b.png)判断某个对象是否含有某个方法。

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/231663bb-71ea-11ef-a343-ba1ea485754b.png)获得迭代器，使用迭代器

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/23fbb5c4-71ea-11ef-8abb-ba1ea485754b.png)tracemalloc是一个内置的模块帮助可以分析内存的使用情况。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/24be6147-71ea-11ef-b996-ba1ea485754b.png)创建一个自己的迭代，这个迭代器，复制读取一个文件的每一行，然后输出。等你需要取出下一行时候会再次读取下一行，如果为空了，就抛出stopiteration的异常。

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/25bf01fb-71ea-11ef-b015-ba1ea485754b.png)你也可以通过编写自己的逻辑实现更加复杂的功能，例如这里的代码，我们希望这个迭代器只返回对于包含了create的行。

‍

一种更加简单的创建迭代器的方法是使用生成器。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/26de27d3-71ea-11ef-8f66-ba1ea485754b.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/27cad1b3-71ea-11ef-8985-ba1ea485754b.png)一个简单的例子

‍

使用生成器完成和上述的代码一样的功能

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/28c13271-71ea-11ef-9da8-ba1ea485754b.png)​

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
