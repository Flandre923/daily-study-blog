---
title: 从uv开始构建Python开发环境。
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/92e65ec9-71ea-11ef-944c-ba1ea485754b.jpg
category: Python
draft: false
---


# 从uv开始构建Python开发环境。

[从 uv 开始构建 Python 开发环境 --- uv から始まる Python 開発環境構築 (zenn.dev)](https://zenn.dev/dena/articles/python_env_with_uv)

为了运行本文中创建的仓库，您需要下载Docker Desktop和VS Code，并在VS Code上安装Dev Container。 此外，我建议您使用以下命令克隆仓库，这将有助于您后续的操作为了运行本文中创建的仓库，您需要下载Docker Desktop和VS Code，并在VS Code上安装Dev Container。

```shell
git clone https://github.com/a5chin/python-uv
```

## 1.1. 实际的操作画面

# 2. 使用 Docker 搭建开发环境

以下主要对 Docker 进行讲解

Dev Container 是因为它将 Docker 容器创建为开发环境

## 2.1. 能够使用 uv

UV 是 Astral 公司在上述 GitHub 仓库中开发的 Python 项目管理工具

因为是使用 Rust [5] 进行开发的，所以运行速度非常快

按照以下流程，在 Docker 容器中能够使用 uv

1. 下载 UV 安装程序
2. 使能够使用 uv，通过路径
3. 更改下载的 uv 的所有者

在 Dev Container 中，由于是 vscode 用户进行操作，建议将下载的 uv 文件夹的所有者更改为 vscode 用户

如果不将所有者从 root 更改，则无法在 VS Code 上修改 uv 的设置文件

```docker
.vscode/Dockerfile ".vscode/ Dockerfile" （注：这部分原文本身就是英文，在某些情况下，可能不需要进行实质意义上的翻译，仅保留原文可能更符合特定情境的需求。这里按照您的要求直接输出了原文。如果您希望对其进行更符合中文表达习惯的处理，比如将 "Dockerfile" 翻译为“Docker 文件”，可以进一步提出需求。）
 FROM debian:bookworm-slim AS builder

 WORKDIR /opt

 # The installer requires curl (and certificates) to download the release archive
 # hadolint ignore=DL3008
 RUN apt-get update && \
     apt-get install -y --no-install-recommends \
         ca-certificates \
         curl

 SHELL [ "/bin/bash", "-o", "pipefail", "-c" ]

 # Download the latest installer
 ADD https://astral.sh/uv/install.sh /uv-installer.sh

 # Run the installer then remove it
 RUN sh /uv-installer.sh && rm /uv-installer.sh

 # uv を使える様に Path を通す
 ENV CARGO_HOME="/opt/.cargo/bin"
 ENV PATH="$CARGO_HOME/:$PATH"

 RUN chown -R vscode $CARGO_HOME
```

## 2.2. 能够使用 Ruff

Ruff 是 Astral 公司在上述 GitHub 仓库中开发的用于 Python 的 Formatter <sup>[[1:3]](https://zenn.dev/dena/articles/python_env_with_uv#fn-1e05-1)</sup> 、Linter <sup>[[2:2]](https://zenn.dev/dena/articles/python_env_with_uv#fn-1e05-2)</sup>

因为是用 Rust [5:1] 编写的，所以速度很快，竟然是 Pylint [6] 的 200 倍以上的速度！

使用 uv 安装通过 .python-version 指定的 Python 以及通过 pyproject.toml 、 uv.lock 指定的包

```docker
  FROM debian:bookworm-slim AS builder

  WORKDIR /opt

  # The installer requires curl (and certificates) to download the release archive
  # hadolint ignore=DL3008
  RUN apt-get update && \
      apt-get install -y --no-install-recommends \
          ca-certificates \
          curl

  SHELL [ "/bin/bash", "-o", "pipefail", "-c" ]

  # Download the latest installer
  ADD https://astral.sh/uv/install.sh /uv-installer.sh

  # Run the installer then remove it
  RUN sh /uv-installer.sh && rm /uv-installer.sh

  ENV CARGO_HOME="/opt/.cargo/bin"
  ENV PATH="$CARGO_HOME/:$PATH"

+ COPY ./.python-version ./pyproject.toml ./uv.lock ./

+ RUN uv python pin "$(cat .python-version)" && \
+     uv sync --dev

  RUN chown -R vscode $CARGO_HOME
```

### 2.3.1. （Ruff）的设置

Ruff 的设置可以在 `ruff.toml`​ 文件中编写设置，基本上是从官方沿用的

然而，上述文档中写道，建议忽略会产生冲突的设置，因此在此补充说明

### 2.3.2. Dev Container 的设置

通过像 `.devcontainer/devcontainer.json`​ 那样设置 Dev Container，在保存时会自动进行格式设置 <sup>[[1:4]](https://zenn.dev/dena/articles/python_env_with_uv#fn-1e05-1)</sup>

```docker
{
    "name": "uv",
    "build": {
        "context": "..",
        "dockerfile": "Dockerfile"
    },
    "features": {
        "ghcr.io/dhoeric/features/hadolint:1": {}
    },
    "customizations": {
        "vscode": {
            "extensions": [
                "charliermarsh.ruff",
                "codezombiech.gitignore",
                "eamodio.gitlens",
                "exiasr.hadolint",
                "kevinrose.vsc-python-indent",
                "mosapride.zenkaku",
                "ms-azuretools.vscode-docker",
                "ms-python.python",
                "njpwerner.autodocstring",
                "oderwat.indent-rainbow",
                "pkief.material-icon-theme",
                "shardulm94.trailing-spaces",
                "usernamehw.errorlens",
                "yzhang.markdown-all-in-one"
            ],
            "settings": {
                "python.defaultInterpreterPath": "/root/.local/share/uv/python",
                "[python]": {
                    "editor.defaultFormatter": "charliermarsh.ruff",
                    "editor.codeActionsOnSave": {
                        "source.fixAll.ruff": "explicit",
                        "source.organizeImports.ruff": "explicit"
                    },
                    "editor.formatOnSave": true
                },
                "files.insertFinalNewline": true,
                "files.trimTrailingWhitespace": true,
                "terminal.integrated.defaultProfile.linux": "zsh",
                "terminal.integrated.profiles.linux": {
                    "zsh": {
                        "path": "/bin/zsh"
                    }
                }
            }
        }
    },
    "postCreateCommand": "uv sync --dev",
    "postStartCommand": "uv run pre-commit install",
    "remoteUser": "vscode"
}
```

# 2.4. 多阶段构建

使用 Docker 的多阶段构建（Multi-stage builds）可以减少 Docker 镜像

在第一阶段的构建中下载所需的软件包，并仅传递第二阶段构建所需的文件

```docker
+ FROM debian:bookworm-slim AS builder

  WORKDIR /opt

  # The installer requires curl (and certificates) to download the release archive
  # hadolint ignore=DL3008
  RUN apt-get update && \
      apt-get install -y --no-install-recommends \
          ca-certificates \
          curl

  SHELL [ "/bin/bash", "-o", "pipefail", "-c" ]

  # Download the latest installer
  ADD https://astral.sh/uv/install.sh /uv-installer.sh

  # Run the installer then remove it
- RUN sh /uv-installer.sh && rm /uv-installer.sh
+ RUN sh /uv-installer.sh


+ FROM mcr.microsoft.com/vscode/devcontainers/base:bookworm

  ENV CARGO_HOME="/opt/.cargo/bin"
  ENV PATH="$CARGO_HOME/:$PATH"

  WORKDIR /opt

+ COPY --from=builder /root/.cargo/bin/uv $CARGO_HOME/uv
  COPY ./.python-version ./

  # sync は devcontainer.json で明示するため不必要
  RUN uv python pin "$(cat .python-version)"
-     uv sync --dev

  RUN chown -R vscode $CARGO_HOME
```

# 3. 赠品

## 3.1. jupyter 分支

我们已经能够对 Jupyter Notebook 进行格式化了

这是主要在使用 Jupyter Notebook 时进行切换的分支

[a5chin/python-uv at jupyter (github.com)](https://github.com/a5chin/python-uv/tree/jupyter)

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
