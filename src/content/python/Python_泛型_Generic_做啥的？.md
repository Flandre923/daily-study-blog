---
title: Python 泛型 Generic 做啥的？
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/b8b84421-71e8-11ef-bafe-ba1ea485754b.png
category: Python
draft: false
---


# Python 泛型 Generic 做啥的？

[Python 泛型 Generic 做啥的？_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV19s421T7DS/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/bfc004e9-71e8-11ef-b78b-ba1ea485754b.png)​

‍

如何限制泛型必须是某个类的子类

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c0e86c23-71e8-11ef-9df4-ba1ea485754b.png)bound

‍

[Python 泛型协变covariant, 逆变contravariant做啥的？_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Tb421p7vd/?spm_id_from=333.788&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c1f9309d-71e8-11ef-b906-ba1ea485754b.png)相当于如果dog是animal是子类型，那么泛型【dog】也是泛型【animal】的子类型。

使用covariant 标志 ，要求夫类型 要涵盖所有的子类型，并子类型要支持夫类型的操作。![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c2b71dff-71e8-11ef-b074-ba1ea485754b.png)例如这里的restock方法，对于dog来说这里的a必须是dog，而对于animal 来说 这个的a可以是animal 依旧是说animal的子类 cat 或者 dog，而子类说明只能是dog。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c3a24051-71e8-11ef-b4ba-ba1ea485754b.png)contravariant 表示 aniaml 会是 dog的子类型， 

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c4ae1f6e-71e8-11ef-a321-ba1ea485754b.png)​

---
本文是个人学习记录，如果有侵权请联系后删除。
