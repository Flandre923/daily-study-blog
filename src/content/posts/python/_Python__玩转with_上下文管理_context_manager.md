---
title: ' Python  玩转with 上下文管理 context manager'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/91c0fe41ff918c2446dd655b6c508219f1fbf9ab54791bebc071f75a87343110.jpg
category: Python
draft: false
---


# [Python] 玩转with 上下文管理 context manager

# [[Python] 玩转with 上下文管理 context manager](https://www.bilibili.com/video/BV1aPYhe7EkN/?spm_id_from=333.788&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/73f932933f08167de811c3e598b42d604d72205fa2c29361eae7d165605d4b4e.png)​

一个方法，返回一个ctxmanager 这个 ctx manager 应该重写 enter 和 exit 的魔法方法 分别表示 with 的进入和退出

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/89fe0cd30334c892c40147bf36c4960f1b90a3c3010c912c5b6e4c4e3c70d02f.png)exit 中的参数是异常处理的参数，enter是with开始时候的内容，返回值会赋值给as后的变量。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0e4100df27af6bc65d0fde4860e67b4602c8e8d571611b68375809ce0da77cb0.png)​

‍

‍

异常处理

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/8a7aeca5c31047eb49dc40ef1aba2bda29f27e1b0526fe00f22f0a32059fd93e.png)异常的类型，异常值，和异常调用栈

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/912b31dd59ff6e10e22a5dc366597a94e8f3368ea1d2bd9ca2c122bbfc2110a1.png)触发异常

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/6ee269314a4e4fe65491cba020927ceb26429dd34001ba18d9f3fd02297c8dae.png)触发异常之后会直接直接进入exit的内容中。之后会直接退出exit，不会再中with中的内容了。

‍

‍

使用装饰器直接实现

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/1e6872c253dd17801b8a4edb411bc7955a48740809ea96596dfaa03b20adcb2c.png)导入

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/9ff66dde50bdcfcf832b0c54c5765f8c19e9d70cb76dbf0807c0768069795112.png)首先运行yield将old path返回给as变量，当with的代码块的内容处理完毕之后会回到这里的os.chdir回到oldpath 中。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/efe5cb8702570814975d153b6b441a406d9e445c6a849ad7640b099640f230e9.png)异常处理

‍

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
