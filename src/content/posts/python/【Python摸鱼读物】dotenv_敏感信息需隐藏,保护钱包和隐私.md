---
title: '【Python摸鱼读物】dotenv 敏感信息需隐藏,保护钱包和隐私'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/44f7686b5cb99fcf02a3492b375f6be77fb30aa1a4630090c1ed2d76893c7ab4.jpg
category: Python
draft: false
---


# 【Python摸鱼读物】dotenv: 敏感信息需隐藏，保护钱包和隐私

# [【Python摸鱼读物】dotenv: 敏感信息需隐藏，保护钱包和隐私_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Vj42197kj/?spm_id_from=333.999.0.0&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

将账号密码api token 等信息直接存储在代码中，是危险的。

一般的做法是存放在环境变量中，不过这很麻烦，而且对于不同的操作系统，操作的方法也不同。

存储敏感信息

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0758114d89cb4922b09dc541ab40ed545a421be9b5fadaea00a25eeafeaf727c.png)​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/02b3acd14f4cc5512905189d797c16eb91ef577701cd0d824a11c6171e717584.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/ef5dda28d1d0cf5870f4a3a73f15086ab2b6ccf6950fbc292df9f0a72ab868aa.png)安装

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/bf35bc00c268ee2085ce0f7e487657cf943ff221dcbb0735568f181ee044958b.png)创建文件

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/cd6f745b378e15df25476d7be34a3c44e3b139dd3e02a2c27b7d457c629d9439.png)存放铭感信息在.env中。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/48eb78648c1ed18e387b325a420fd241f04e6fe18f45a0e482cb702485fec8b3.png)使用

如果你不是用默认的文件名的话，可以通过给load_dotenv指定对于的文件名称

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0c3539146a97ddc48ee1096cc8cee85cc38e6ba3c1591bc66f273165853d121c.png)​

如果使用git

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/7ae752c1d01d7c33993299be07df777ac94413059412965c39c34ee430fa085a.png)别忘记添加。将所有的.env文件忽略掉。

‍

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
