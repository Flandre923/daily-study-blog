---
title: 【Python摸鱼读物】dotenv 敏感信息需隐藏，保护钱包和隐私
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/29d7b38a-71ea-11ef-96ba-ba1ea485754b.jpg
category: Python
draft: false
---


# 【Python摸鱼读物】dotenv: 敏感信息需隐藏，保护钱包和隐私

# [【Python摸鱼读物】dotenv: 敏感信息需隐藏，保护钱包和隐私_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Vj42197kj/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

将账号密码api token 等信息直接存储在代码中，是危险的。

一般的做法是存放在环境变量中，不过这很麻烦，而且对于不同的操作系统，操作的方法也不同。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/2ec123d1-71ea-11ef-b51b-ba1ea485754b.png)存储敏感信息

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/2f59f8d9-71ea-11ef-b714-ba1ea485754b.png)​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3033f8c3-71ea-11ef-993e-ba1ea485754b.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/30e04e69-71ea-11ef-b6f8-ba1ea485754b.png)安装

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/31a15ef3-71ea-11ef-bd6c-ba1ea485754b.png)创建文件

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/32791368-71ea-11ef-bf65-ba1ea485754b.png)存放铭感信息在.env中。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/3337c4bd-71ea-11ef-a60f-ba1ea485754b.png)使用

如果你不是用默认的文件名的话，可以通过给load_dotenv指定对于的文件名称

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/34399eb2-71ea-11ef-9610-ba1ea485754b.png)​

如果使用git

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/34f764fd-71ea-11ef-b633-ba1ea485754b.png)别忘记添加。将所有的.env文件忽略掉。

‍

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
