---
title: '【Python】为什么不应该将列表作为函数的默认参数？'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/d2044912ebcf4e8c8a093499b23813ca94487e29d47685c43454c7bc51fac178.jpg
category: Python
draft: false
---


# 【Python】为什么不应该将列表作为函数的默认参数？

[【Python】为什么不应该将列表作为函数的默认参数？_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1st42177YR/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c3fb4c622c645f64af1e63a77cfcf4ecd27b9e556c0d759221917f763eaa7d1a.png)这里可以看到出现了1，2的一个list，这是不应该的，说明了这里的引用是同一个list。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/e4c45757f8852faa86b07d5908d33c90fabfd7a6c9f0168c448315aa07615d14.png)通过id可以确定一个唯一的实例的对象，如果是一致的说明是同一个对象。

不要使用任何的默认的可变引用对象作为默认数值。正常的处理应该这样

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/8c176bc1974c62a4edb92ad9bdaae14f670bef545c2abafcbdcf264b9820535f.png)​

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
