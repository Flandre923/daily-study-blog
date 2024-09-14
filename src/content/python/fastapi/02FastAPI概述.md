---
title: 02FastAPI概述
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/a384e36c-71ea-11ef-808f-ba1ea485754b.jpg
category: Python
draft: false
---


# 02FastAPI概述

**第02章 FastAPI概述**作者：smithonisan 更新日期：2021.08.14

**本章目录**

* 关于FastAPI
* 与Flask的比较

**关于FastAPI**在Python世界中，像Django这样的大规模Web框架，以及像Flask和Bottle这样的微型框架，早已广受欢迎。作为备受期待的新星，FastAPI登场了。

让我们先来看看FastAPI的特点。

* 根据请求和响应的模式定义自动生成Swagger UI文档
* 通过明确定义上述模式，实现类型安全的开发
* 支持ASGI，因此可以执行异步处理，速度快

FastAPI在多种情况下都非常活跃。近年来，随着机器学习的兴起，FastAPI经常被选择用于提供使用Python的机器学习服务。即使在构建API的预测阶段，机器学习处理往往需要较多的时间和负荷，因此异步处理的高速性能将得到充分利用。

另一方面，作者认为，在启动公司或新Web服务的启动等情况下，FastAPI可能发挥更大的力量，特别是当与SPA（单页应用程序）结合使用，作为后端运行的Web API时。

正如前文所述，FastAPI定义了请求和响应的模式。这使得前端工程师可以轻松自动生成实现时使用的文档，并且实际上还可以更改请求参数并尝试调用API。

通过先定义模式来确定前端和后端之间的接口，并同时启动各自的开发方式，通常被称为“模式驱动开发（Schema-Driven Development）”。

使用FastAPI，即使没有专业知识或事先了解，也可以自然地开始模式驱动开发，而不会有任何不适感。通过模式驱动开发，可以减少集成前端和后端时由于规格误解等导致的问题，从而提高开发速度。

在Web服务的后端开发中，FastAPI不仅可以提高开发速度，在后续阶段也能发挥作用。你可能已经意识到了，随着Web服务被越来越多的用户使用，经常会遇到扩展问题。

FastAPI不仅类型安全，而且速度快。

在Web开发世界中，开发速度和产品寿命之间的权衡经常是一个问题，但FastAPI的性能可以与Go等静态类型语言相媲美，可以创建在服务扩展阶段也能充分承受的API。

在本书中，我们将以TODO应用程序为例，介绍FastAPI的魅力。在开发中，经验是一个重要因素。请不要客气，通过模仿或复制和粘贴来接触代码。我们期待更多的人能够掌握FastAPI中的Web API开发。

**与Flask的比较**Flask是一个自2010年以来一直在开发的Python轻量级Web框架（微框架）。

正如FastAPI的官方文档所描述的，FastAPI也受到了Flask的很大影响。

Flask是一个非常方便的框架，用于简单地创建API。然而，FastAPI作为后来者，拥有上述Flask所没有的特点：

* 自动生成Swagger UI文档
* 类型安全
* 高速

关于“高速”，有FastAPI与Flask的基准测试结果，请参考。

---
本文是个人学习记录，如果有侵权请联系后删除。
