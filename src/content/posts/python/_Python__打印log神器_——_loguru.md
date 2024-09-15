---
title: ' Python  打印log神器 —— loguru'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/e241f1d16f584de09d2253c7f794d358815202e44300a97565ab58ba3f93a7f3.jpg
category: Python
draft: false
---


# [Python] 打印log神器 —— loguru

[[Python] 打印log神器 —— loguru_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1VnW7edEq7/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c5db79064530254b3ad714dfa81620404d5f31839c7d29cbd41bae89b7343cd3.png)安装

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/481229239ad51c5da6daf185fd44420b369323d9f4517130cc50314a07174e48.png)导入

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/78ed7516e43dbb478383fc40e5c2fd1cd5b1c5ab408a42b451954dfb54af96a7.png)日志等级

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/9f6a9d8b1adb56193c67285a2d091f3c524c02ae50792bd33323dd1742ba3d17.png)默认输出

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/dded976e8a46d026da110b3fc32db9d180c48b301702219c7dda927f6d7fa547.png)生成一个msg.log的文件记录了日志的信息。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/e984c677edf1843ef703dd1bea7a086f509b03fa6e371ad969e63da6a724e37b.png)移除所有配置，控制台不在显示日志内容。

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/e37353b30edb2bbfa7a458646c75ebb2ba75f3ed6f77f652bc83e3707d360c1a.png)删除指定的id的配置

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/a6f1bbe944fed02b91d20888b3fdf4c3be10553d86429a1a238af73cc9a30c4e.png)调整日志的输出等级。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/4cc03c67ad93384bcac052a3e44b66a5bc726af413805323e29c822d05a41a46.png)调整日志的格式

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c0110df9c1896d7b6aa17d8a009f749fbc45fdb66b0ee87d1268b5148c70252c.png)输出到控制台，并加上背景色。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/ffeaac93901aa9aeb667400f9d716ea919adf657a8883dc8827e7994f22674e7.png)自动加上对应的等级的背景色。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/180bc69cff78560a64eee27135e32e43bdb3d26962e01a088f625d25c7025cb5.png)而对应的父log则不会附加bind的信息。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f4362e5dbc86abfeaeb17a213c901953104c678cdceb68e6f3c321efc3df027a.png)通过上下文管理附加打印信息。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f787e76265ffa1420e57ec2bdf31c4bfda3ea83363d69cd986d2736cc5bdb0b3.png)​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3089fccdd494f16fad666f41b7ade7d94f196a9d314723be309f4d395baa6abe.png)使用装饰器给函数内的所有的日志输出附加信息。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/6c952fc026b72fbc503418f002a8afa0a1f8e5c0134068ce14f810ddb81fd411.png)exception方法会捕获整个调用栈并打印。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c1f93c63c2ec3b8fc39a37d2fd8a961461184d50c342ce98e80c3ef9d5051daa.png)自动记录异常

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/9bb632215ccad0e503766dd44149ad98f0dfc7d30098be3e99a2a829afb11150.png)捕获指定的异常

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/dc2c42676602e2a4ca6fc68cb5bea70e6d63cf73bf96f298c3e3331738e496d1.png)记录异常，并且调整记录的等级。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/b9018d5e83471fba957b327bf2ce618b8b5111c0b6ec951daaa49e8ea3ad745b.png)同样可以作为装饰器。

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
