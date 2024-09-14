---
title: [Python] 打印log神器 —— loguru
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0fc30c23-71e9-11ef-8ea7-ba1ea485754b.jpg
category: Python
draft: false
---


# [Python] 打印log神器 —— loguru

[[Python] 打印log神器 —— loguru_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1VnW7edEq7/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/23eb1048-71e9-11ef-af10-ba1ea485754b.png)安装

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/2489666d-71e9-11ef-a653-ba1ea485754b.png)导入

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/2576ad02-71e9-11ef-bb07-ba1ea485754b.png)日志等级

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/26482f5b-71e9-11ef-84f5-ba1ea485754b.png)默认输出

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/27289c28-71e9-11ef-8667-ba1ea485754b.png)生成一个msg.log的文件记录了日志的信息。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/281f85f8-71e9-11ef-afbf-ba1ea485754b.png)移除所有配置，控制台不在显示日志内容。

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/29270914-71e9-11ef-9941-ba1ea485754b.png)删除指定的id的配置

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/29db2c04-71e9-11ef-9b05-ba1ea485754b.png)调整日志的输出等级。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/2aaf6f4f-71e9-11ef-8ceb-ba1ea485754b.png)调整日志的格式

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/2b9360e2-71e9-11ef-b030-ba1ea485754b.png)输出到控制台，并加上背景色。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/2c902e7d-71e9-11ef-b9a3-ba1ea485754b.png)自动加上对应的等级的背景色。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/2e442e7e-71e9-11ef-b764-ba1ea485754b.png)而对应的父log则不会附加bind的信息。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/2f794834-71e9-11ef-9ea1-ba1ea485754b.png)通过上下文管理附加打印信息。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/307b708e-71e9-11ef-8c39-ba1ea485754b.png)​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/318e45b5-71e9-11ef-9f9c-ba1ea485754b.png)使用装饰器给函数内的所有的日志输出附加信息。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3274d106-71e9-11ef-8246-ba1ea485754b.png)exception方法会捕获整个调用栈并打印。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/33739c94-71e9-11ef-8481-ba1ea485754b.png)自动记录异常

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/343f6179-71e9-11ef-9be5-ba1ea485754b.png)捕获指定的异常

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/34f56dd9-71e9-11ef-8a71-ba1ea485754b.png)记录异常，并且调整记录的等级。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/35fc05f2-71e9-11ef-8dcb-ba1ea485754b.png)同样可以作为装饰器。

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
