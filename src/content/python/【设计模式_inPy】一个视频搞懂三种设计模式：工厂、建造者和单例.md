---
title: 【设计模式 inPy】一个视频搞懂三种设计模式：工厂、建造者和单例
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/4fc008e9-71ea-11ef-a5b1-ba1ea485754b.jpg
category: Python
draft: false
---


# 【设计模式 inPy】一个视频搞懂三种设计模式：工厂、建造者和单例

[【设计模式 inPy】一个视频搞懂三种设计模式：工厂、建造者和单例_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV131421876N/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/5131caea-71ea-11ef-9b0a-ba1ea485754b.png)存在的问题是，这个数据库的连接参数存在多个位置的，如果出问题修改是需要再多个位置修改的， 并且代码存在重复。

‍

更改为工厂模式

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/527c4fa1-71ea-11ef-b044-ba1ea485754b.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/53af1dec-71ea-11ef-b8e5-ba1ea485754b.png) client改写

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/54bb99d4-71ea-11ef-9cd5-ba1ea485754b.png)创建一个配置文件，将内容放置到配置文件中。

‍

‍

# 建造者模式

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/558c8cee-71ea-11ef-92fe-ba1ea485754b.png)​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/56a545ec-71ea-11ef-8a82-ba1ea485754b.png)像这种要传入大量的参数的类，可以使用builder方法。

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/5792a002-71ea-11ef-85b0-ba1ea485754b.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/586fd65d-71ea-11ef-b5a0-ba1ea485754b.png)再build中创建实例。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/595f0673-71ea-11ef-b5d6-ba1ea485754b.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/5a022e46-71ea-11ef-8463-ba1ea485754b.png)调用

‍

# 单例

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/5acdccdf-71ea-11ef-a644-ba1ea485754b.png)new 方法是object的方法， 是创建类的方法，然后new回去调用init，一般情况下是不需要去重写new的。参数中的cls表示当前的类。

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
