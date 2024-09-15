---
title: 'Python 泛型 Generic 做啥的？'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f749c80ed1915df813c3f0ab92b1bf4d8a2ac25e9c41483c7a75e75a98dd0c70.png
category: Python
draft: false
---


# Python 泛型 Generic 做啥的？

[Python 泛型 Generic 做啥的？_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV19s421T7DS/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/67592e9f8d343447e7a8c1dde18e2ac8c20dfa0ff2ce431480bd461855a2a70a.png)​

‍

如何限制泛型必须是某个类的子类

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/cf95570b7a5675f0a89a478b3752eea96c6aa879e19c4fc07f52b2771114315b.png)bound

‍

[Python 泛型协变covariant, 逆变contravariant做啥的？_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Tb421p7vd/?spm_id_from=333.788&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/e680eb3e33a2eba412690741092b52039c7aad0f6299ee31afe18d43ead18bdf.png)相当于如果dog是animal是子类型，那么泛型【dog】也是泛型【animal】的子类型。

使用covariant 标志 ，要求夫类型 要涵盖所有的子类型，并子类型要支持夫类型的操作。![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/1f37f1aa915a52581fec956553e303b6ec0a6809c74f9ee0f63e6f011e88f5ed.png)例如这里的restock方法，对于dog来说这里的a必须是dog，而对于animal 来说 这个的a可以是animal 依旧是说animal的子类 cat 或者 dog，而子类说明只能是dog。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/4fde2c09ffb69cf4b5462cddaa8b121bffabaafd31bdc368019ede9b3d16f108.png)contravariant 表示 aniaml 会是 dog的子类型， 

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/dda731982a37c67e3a8fef5df2a537e58e8936a78a4ddeb1b279fc18e435099c.png)​

---
本文是个人学习记录，如果有侵权请联系后删除。
