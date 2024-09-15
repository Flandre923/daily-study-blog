---
title: '使用uv单独管理Python项目。'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/d9cbe4d1155dd2c2698fb9f704fe9a0d4d63d6b2e83d4154d3ff98f8e7c7b018.png
category: Python
draft: false
---


# 使用uv单独管理Python项目。

# 1. UV 的基本操作

UV 的官方文档由 [UV](https://docs.astral.sh/uv/) 进行整理。

## 1.1 uv的安装

可以按照公式的 uv - Getting started 进行安装。对于 mac OS 或 Linux 系统，情况如下。

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

安装后，通过 `exec $SHELL -l`​ 等操作重新加载 shell 后，即可启动 uv。此次使用的 uv 版本如下。

```docker
uv --version
> uv 0.3.1
```

此外，也可以从 [PyPI ](https://pypi.org/project/uv/)安装 uv 。

```docker
pip install uv
```

```docker
pipx install uv
```

## 1.2 新规划项目的初始化

像 Rye 一样，可以使用 `init`​ 创建新的项目。 `my-project`​ 是任意的项目名称。如果已经在想要创建的项目下，则仅使用 `uv init`​ 就可以创建。

```docker
uv init my-project
cd my-project
```

然后，会创建以下目录结构，并且 pyproject.toml 也会自动生成。

```docker
.
├── README.md
├── pyproject.toml
└── src
    └── my_project
        └── __init__.py
```

​`pyproject.toml`​ 的内容如下。

```docker
[project]
name = "my-project"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.12"
dependencies = []

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

```

## 1.3 软件包的同步

将基于 `pyproject.toml`​ 安装软件包。可以执行以下命令。

```docker
uv sync
```

像rye一样，作为虚拟环境创建了 `.venv`​ ，并且生成了名为 `uv.lock`​ 的锁定文件。此外，如果要重新安装所有软件包，可以通过 `uv sync --reinstall`​ 实现。

## 1.4 虚拟环境的激活

可以通过以下命令启用虚拟环境。

```docker
. .venv/bin/activate
```

若要使其无效，请执行以下操作。

```docker
deactivate
```

‍

## 1.5 Python 版本变更

像 Rye 一样，可以使用 pin 命令更改 Python 的版本。也会生成 .python-version 文件。

```docker
uv python pin 3.10
```

另外，在初始化项目时，在 uv init 的参数中指定 --python 或 -p 的版本即可。

```docker
uv init my-project-3.10 -p 3.10

```

或者，也可以像直接将 `pyproject.toml`​ 的 `requires-python = ">=3.10,<3.11"`​ 那样进行改写，并在 `uv sync`​ 中进行更新。

详细信息请参考官方的[ uv - Python](https://docs.astral.sh/uv/concepts/python-versions/) 版本。

## 1.6 软件包的添加

可以使用 uv add 添加软件包。接下来我们将安装 numpy。

```docker
uv add numpy

```

也可以指定版本。

```、
uv add "numpy==1.26.4"
```

也可以用 `uv remove`​ 去除包装。

```、
uv remove numpy

```

如果已经存在 `requirements.txt`​ ，也可以从 `uv add -r`​ 进行安装。

```、
uv add -r requirements.txt
```

此外，也可以作为开发用的依赖包通过 --dev 进行安装。

```、
uv add jupyterlab --dev
```

​`pyproject.toml`​ 以下内容将被添加。

```、
[tool.uv]
dev-dependencies = [
    "jupyterlab>=4.1.6",
]
```

安装的软件包可通过 uv pip list 进行确认。

# 1.7 运行

在不启用虚拟环境的情况下执行特定脚本时，可以通过 `uv run`​ 来执行。例如，当存在以下作为 `main.py`​ 的脚本时，

```、
print("Hello!")
```

可以通过以下命令执行。

```、
uv run main.py
```

# 2. uv 的便利功能

## 2.1 通过 uv venv 创建虚拟环境

即使不是 `uv init`​ ，也可以仅创建虚拟环境。可以通过参数指定目标路径，如果未指定，则在当前目录中创建 `.venv`​ 。如果已经存在虚拟环境，则将其删除并创建新的虚拟环境。

```、
uv venv my-project-venv
```

可以使用 `--python`​ 或 `-p`​ 来指定 Python 的版本。

```、
uv venv -p 3.10
```

如果要添加软件包，可以通过 uv pip install 进行安装。

```、
uv pip install numpy
```

安装的软件包可通过 uv pip list 进行确认。

请参考官方的 uv [- The pip 接](https://docs.astral.sh/uv/pip/)口来进行这些一系列操作。

## 2.2 使用 uvx 调用工具

​`uvx`​ 可以在不安装工具的情况下被调用。例如，可以通过以下方式调用快速的 Python 代码检查器和代码格式化工具 ruff。请注意，下面的命令与 `uv tool run ruff`​ 相同。

```、
uvx ruff

```

可以在特定版本中运行。

```、
uvx ruff@0.3.0 check
```

```、
uvx ruff@latest check
```

特别是在 `ruff`​ 等情况下，会使用该项目下的 `pyproject.toml`​ 的设置。ruff 和 mypy 等的设置请以此作为参考。

请查看官方的 uv - Using tools 以了解 `uvx`​ 的[详细信息](https://docs.astral.sh/uv/guides/tools/)。

# 2.3 安装在 PyPI 中无法使用的软件包

按照公式的 uv - Specifying dependencies 的 Dependency sources 中所记载的方法，可以安装 Git、URL、本地 wheel 路径等。例如，如果要通过 URL 指定特定的 wheel，可以像下面这样操作。

```、
 uv add https://files.pythonhosted.org/packages/f7/29/13965af254e3373bceae8fb9a0e6ea0d0e571171b80d6646932131d6439b/setuptools-69.5.1-py3-none-any.whl

```

​`pyproject.toml`​ 中将新添加 `[tool.uv.sources]`​ 。

```、
dependencies = [
    "setuptools",
]

[tool.uv.sources]
setuptools = { url = "https://files.pythonhosted.org/packages/f7/29/13965af254e3373bceae8fb9a0e6ea0d0e571171b80d6646932131d6439b/setuptools-69.5.1-py3-none-any.whl" }
```

## 2.4 [tool.hatch.build.targets.wheel] 进行的模块访问

像Rye一样，将 `[tool.hatch.build.targets.wheel]`​ 记录在 `pyproject.toml`​ 中，就可以在不考虑目录结构的情况下导入模块。

```、
[tool.hatch.build.targets.wheel]
packages = ["src/my_project", "src"]
```

## 2.5 设置用于安装依赖 CUDA 的 PyTorch 的 extra-index-url

在参考安装 PyTorch 旧版本的基础上，为与 CUDA 版本匹配的 URL 添加 `pyproject.toml`​ 的 `extra-index-url`​ 。 

```、
[tool.uv]
extra-index-url = ["https://download.pytorch.org/whl/cu121"]
```

追加后，可以使用以下命令安装依赖 CUDA 的 PyTorch。

```、
uv add "torch==2.4.0+cu121"
```

也可以指定为 `index-url`​ ，但默认指定为 `"[https://pypi.org/simple](https://pypi.org/simple)"`​ 。如果需要提高优先级，似乎可以像下面这样记载。关于详细内容，请参考 uv - [Settings#index - url 。](https://docs.astral.sh/uv/reference/settings/#index-url)

```toml
[tool.uv]
index-url = "https://download.pytorch.org/whl/cu121"
extra-index-url = ["https://pypi.org/simple"]
```

find-links 也可以像 [tool.uv] 一样进行设置。

另外，如果要根据每个架构更改要安装的软件包，这篇文章很有参考价值。

[uvでPyTorchのCPU / CUDAバージョンを環境ごとに管理する (zenn.dev)](https://zenn.dev/mjun0812/articles/b22adf3fab1fdd)

## 2.6 与其他软件的协作

在公式的[ uv - ]()​[ Integration guides](https://docs.astral.sh/uv/guides/integration/)中，记载了在 Docker、Github Action、Pre-commit 等中整合 uv 时的最佳实践。

## 2.7 flash-attention 进行安装

[flash-attention](https://github.com/Dao-AILab/flash-attention) 是一种用于快速处理 transformer 模型的技术，并已打包为 flash-attn。

我们在下面总结了使用（uv）进行安装的方法。

# 3. 结语

似乎仅用 uv 就能完成 Python 项目管理了。原本，与 Rye 相比，uv 的一个优点是，会在锁定文件中生成支持跨平台的 wheel 的 URL。通过此次更新，它变得可以像使用 Rye 一样具有相同的操作感，恐怕在图灵中，Python 项目管理将主要使用 uv

此次更新及官方文档已发布，因此可能存在一些尚不了解的功能，我们会适时添加那些看似便利的功能。另外，由于所介绍的功能可能存在错误，若您能在评论中指出，我们将不胜感激。

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
