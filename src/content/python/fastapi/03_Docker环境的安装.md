---
title: 03 Docker环境的安装
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/a9d93883-71ea-11ef-8eef-ba1ea485754b.jpg
category: Python
draft: false
---


# 03 **Docker环境的安装**

**第03章 Docker环境的安装**

**本章目录**

* docker-compose的安装

  * 1. 排除环境差异
  * 2. 封装环境
* 安装
* 确认

在本章中，我们将解释使用Docker作为开发环境的意义，并进行Docker的安装。 如果您已经熟悉Docker开发，可以跳过本章，继续进行下一章关于创建Docker镜像的内容。

### docker-compose的安装

在本书中，我们决定通过docker-compose使用Python和FastAPI。

Docker是一个提供容器服务的应用程序。我们不直接安装Python，而是选择在Docker中安装，原因有两个：

1. 排除环境差异
2. 封装环境

让我们详细看看每个原因。

1. **排除环境差异**读者中可能有人使用Mac，也有人使用Windows或Linux。根据不同的操作系统，Python的版本可能会有所不同，有时Python的包库也可能依赖于这些环境。  
    Python允许在同一个操作系统中安装多个版本，并在它们之间切换。切换方法会根据设置环境的库而有所不同（例如Pyenv、Virtualenv（venv）、Pipenv等）。然而，切换方法并没有一个事实上的标准，而且很难为所有读者准备最合适的方法。  
    使用Docker，可以固定Python运行的操作系统和包含当前创建的API的底层环境，从而大大减少环境差异。这样，在阅读本书的过程中，安装时的错误或特定命令的错误将会减少。
2. **封装环境**另外，在本书的第11章“数据库连接和数据库模型（Models）”中，我们将安装MySQL。像MySQL这样的数据库往往更依赖于比Python运行环境更底层的API、操作系统或硬件环境。在这里，Docker可以吸收环境差异。此外，通过将Python执行容器和MySQL容器分开，可以明确这些容器之间的依赖关系。  
    使用Docker，可以将Python或数据库环境封闭在容器内部，因此在出错时可以轻松地重新创建或废弃容器，最终不会污染宿主机的环境。

使用docker-compose是本书的一个主要目标，以确保内容可以顺利执行，而不会出现额外的问题。不仅如此，使用相同的方法，团队也可以共享API，因此在实际的团队开发中也会非常有用。

### 安装

让我们立即安装docker-compose。如果已经安装，请继续安装Python和FastAPI。

关于docker-compose的安装，请参考Docker的官方文档。

对于Mac用户，通过安装Docker for Mac，可以同时安装docker-compose。对于Windows用户，安装Docker for Windows也可以同时安装docker-compose。Linux用户可以通过curl下载二进制文件进行安装。

### 确认

让我们确认docker-compose是否已安装。

在shell中输入：

```shell
$ docker-compose version
```

如果返回类似以下的版本信息，则表示安装成功（版本可能因安装环境和时间而异）：

```text
docker-compose version 1.29.0, build 07737305
docker-py version: 5.0.0
CPython version: 3.9.0
OpenSSL version: OpenSSL 1.1.1h  22 Sep 2020
```

在下一章中，我们将使用docker-compose安装Python和FastAPI。

---
本文是个人学习记录，如果有侵权请联系后删除。
