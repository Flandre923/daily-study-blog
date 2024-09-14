---
title: [Python] 玩转with 上下文管理 context manager
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/36fccde3-71e9-11ef-a897-ba1ea485754b.jpg
category: Python
draft: false
---


# [Python] 玩转with 上下文管理 context manager

# [[Python] 玩转with 上下文管理 context manager](https://www.bilibili.com/video/BV1aPYhe7EkN/?spm_id_from=333.788&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/38b84caf-71e9-11ef-a023-ba1ea485754b.png)​

一个方法，返回一个ctxmanager 这个 ctx manager 应该重写 enter 和 exit 的魔法方法 分别表示 with 的进入和退出

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/396f30a3-71e9-11ef-828d-ba1ea485754b.png)exit 中的参数是异常处理的参数，enter是with开始时候的内容，返回值会赋值给as后的变量。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3a7b4a9d-71e9-11ef-892b-ba1ea485754b.png)​

‍

‍

异常处理

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3b906b36-71e9-11ef-bc0c-ba1ea485754b.png)异常的类型，异常值，和异常调用栈

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3ca0a6a4-71e9-11ef-90fa-ba1ea485754b.png)触发异常

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3d9c2757-71e9-11ef-9fab-ba1ea485754b.png)触发异常之后会直接直接进入exit的内容中。之后会直接退出exit，不会再中with中的内容了。

‍

‍

使用装饰器直接实现

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3e6369b9-71e9-11ef-9c96-ba1ea485754b.png)导入

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3f497f93-71e9-11ef-8b89-ba1ea485754b.png)首先运行yield将old path返回给as变量，当with的代码块的内容处理完毕之后会回到这里的os.chdir回到oldpath 中。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/403a4aed-71e9-11ef-916a-ba1ea485754b.png)异常处理

‍

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
