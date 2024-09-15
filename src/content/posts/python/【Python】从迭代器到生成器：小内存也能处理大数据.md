---
title: '【Python】从迭代器到生成器：小内存也能处理大数据'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/45e119bf9432c6fdd9728fbdface693638d769685f19a02c5b13695273174f71.jpg
category: Python
draft: false
---


# 【Python】从迭代器到生成器：小内存也能处理大数据

[【Python】从迭代器到生成器：小内存也能处理大数据_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1jt421c7yN/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3d09fd22d08e75b20cd275c91395815f9b15e5f3532ef4fae1a7620a7e12ec37.png)判断某个对象是否含有某个方法。

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/a04a73db7981a43365118632c6d2c9c971a396901142a2635927f0ebea64b7ba.png)获得迭代器，使用迭代器

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/9706d7e7ef451a89c722851935fdde41619379fa4fbe960a7d96bfb45ef22e37.png)tracemalloc是一个内置的模块帮助可以分析内存的使用情况。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/42f69f50c02b27f599ad5734f07647b6b76e2cb1eb807e61b32de29c54babb5c.png)创建一个自己的迭代，这个迭代器，复制读取一个文件的每一行，然后输出。等你需要取出下一行时候会再次读取下一行，如果为空了，就抛出stopiteration的异常。

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/44f0fc1969cde65d894da6a0db5af41ad33ccd60ad4ddfd6bc9b2b40b939cfb1.png)你也可以通过编写自己的逻辑实现更加复杂的功能，例如这里的代码，我们希望这个迭代器只返回对于包含了create的行。

‍

一种更加简单的创建迭代器的方法是使用生成器。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/aafcfa5fb088eae86238164f236289434bc128b880880c2f2db6c50819d0b734.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/365119e268ac6677600d1f58a3fcda3c454215fe9150be98ad80d6988b763f0c.png)一个简单的例子

‍

使用生成器完成和上述的代码一样的功能

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/55cc8000398f96996cc8b0909fbd96afcd8ab021cab4e40423d8058bfb295352.png)​

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
