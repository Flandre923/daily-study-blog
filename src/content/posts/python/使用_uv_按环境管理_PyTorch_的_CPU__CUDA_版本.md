---
title: '使用 uv 按环境管理 PyTorch 的 CPU  CUDA 版本'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/b29db418db1cf4309dc5e31ddb9c87597bffab0bc150c47526178217bec78623.jpg
category: Python
draft: false
---


# 使用 uv 按环境管理 PyTorch 的 CPU  CUDA 版本

命令体系与 Rye 几乎相同，可以像下面这样构建喜欢的 Python 环境版本。

```toml
uv python install 3.11
uv python pin 3.10
```

在 poetry 中，可以考虑多平台进行依赖关系解决和软件包安装，但依赖关系的解决速度较慢，而在 Rye 中，由于依赖关系的解决是基于 Rust 实现的，速度较快，但会创建依赖于特定机器环境的 requirements.lock，存在难以管理跨多个环境的项目的问题。

因此，我认为由于能够考虑多平台的 uv 吸收了 Rye 的 Python 管理功能，就像 poetry 一样，双方的用户应该能够毫无问题地进行迁移。

我想通过此功能添加来迁移在 poetry 和 Rye 中管理的项目，并一直在尝试错误地探索 PyTorch 的安装方法。

因此，我们发现了一种可以像 poetry 的环境标记一样，根据环境切换安装 PyTorch 的方法，在此与大家分享。

首先，以下展示最先完成的 pyproject.toml 。

```toml
[project]
name = "new-uv"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.11"
dependencies = [
    "torch==2.4.0+cu118; sys_platform == 'linux' and platform_machine == 'x86_64'",
    "torch==2.4.0; sys_platform == 'darwin' or (sys_platform == 'linux' and platform_machine == 'aarch64')",
    "torchvision==0.19.0+cu118; sys_platform == 'linux' and platform_machine == 'x86_64'",
    "torchvision==0.19.0; sys_platform == 'darwin' or (sys_platform == 'linux' and platform_machine == 'aarch64')",
    "numpy<2.0.0",
]

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[tool.uv]
find-links = [
    "https://download.pytorch.org/whl/cu118/torch",
    "https://download.pytorch.org/whl/cu118/torchvision",
]
```

上述的 pyproject.toml 是在以下环境中进行验证的。

* macOS 14.6 Sonoma，arm64，M1 MacBook Air 2020
* Ubuntu 24.04，aarch64，Docker 容器（在上述 macOS 上）
* Ubuntu 22.04，x86_64，锐龙 5700 + RTX3090 的组装电脑

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
