---
title: [Python] 啊？Python还有弱引用？
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/06cd3b09-71e9-11ef-872d-ba1ea485754b.png
category: Python
draft: false
---


# [Python] 啊？Python还有弱引用？

# [[Python] 啊？Python还有弱引用？](https://www.bilibili.com/video/BV1ev8Je1EH5/?spm_id_from=333.788&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

强引用是指一般的引用，例如![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0a306948-71e9-11ef-84f4-ba1ea485754b.png)，这里的u1，u2就是强引用，强引用只要还存在着引用，这个内存就不会被GC回收。

弱引用就是和强引用相对应的，只要这个实例没有强引用，那么这个弱引用就会被回收，并且存在的数据结构也会被删除。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0ad800e2-71e9-11ef-8f00-ba1ea485754b.png)导入包

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0b812008-71e9-11ef-995a-ba1ea485754b.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0c47158b-71e9-11ef-adec-ba1ea485754b.png)当chat room被方法运行结束之后，那么对应的user的强引用就没有了，那么自然对应的字典的是弱引用的， 那么就会被gc回收。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0cf863f9-71e9-11ef-9070-ba1ea485754b.png)​

‍

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0db2a57a-71e9-11ef-9560-ba1ea485754b.png)python提供的弱引用

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0ea7577a-71e9-11ef-ba84-ba1ea485754b.png)单独创建弱引用

‍

数字，字符串等不支持弱引用

‍

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
