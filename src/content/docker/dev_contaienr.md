---
title: dev contaienr
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Docker']
description: Docker学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/5482d926-71e8-11ef-bc27-ba1ea485754b.png
category: Docker
draft: false
---


# dev contaienr 

‍

# 构建一个Node环境

(Ctrl+Shift+P)

Dev containers:Add Dev Containers Configuration Files...

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/6bf46b7b-71e8-11ef-8f6c-ba1ea485754b.png)​

NodeJS & TypeScript

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/6ccb5c10-71e8-11ef-90fa-ba1ea485754b.png)版本

添加开发的CLI，这里不选择任何的内容

你将会得到一个

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/6db347e9-71e8-11ef-904d-ba1ea485754b.png)​

这样的json

‍

# 存在devcontainer如何打开

1. 安装了vscode
2. 安装了docker
3. 确保安装dev container插件
4. ctrl+shift+p 然后reopen in container

# 退出容器

点击绿色的按钮，然后选择“Reopen Folder Locally”

# 官方提供的各种容器

[Templates (containers.dev)](https://containers.dev/templates)

‍

# 启动时候自动给vscode增加插件 增加设置

```gdscript
{
  ...
  "customizations": {
	"settings": { # 添加配置
	  "editor.formatOnSave": true,
	  ...
	}
    "vscode": {
      "extensions": [ # 添加插件
        "dbaeumer.vscode-eslint",
        "esbenp.prettier-vscode",
        "stylelint.vscode-stylelint"
      ]
    }
  }
}
```

# 通过feature指定只用的软件

```gdscript
{
    "name": "Java Development",
    "image": "mcr.microsoft.com/devcontainers/base:ubuntu",
    "features": {
        "ghcr.io/devcontainers/features/git:1": {
            "version": "latest",
            "ppa": "false"
        },
        "ghcr.io/devcontainers/features/java:1": {
            "version": "21",
            "jdkDistro": "amzn",
            "installMaven": "true",
            "mavenVersion": "3.9.7",
            "installGradle": "false"
        }
    },
    "containerEnv": {},
    "customizations": {
        "vscode": {
            "settings": {},  # 自定义设置
            "extensions": [
                "vscjava.vscode-java-pack"
            ]
        }
    }
}
```

‍

# 指定运行的用户

```gdscript
{
    "name": "Java Development",
    "build": {
        "dockerfile": "./Dockerfile",
        "context": "."
    },
    "remoteUser": "root" # 指定运行的用户是root
}
```

# 配置端口转发

```gdscript
//devcontainer.json
{
  "name": "Node.js",
。。。。
  // "forwardPorts": [3000],

  "portsAttributes": {
    "3000": {
      "label": "Hello Remote World",
      "onAutoForward": "notify"
    }
  },

}

```

# 配置结束之后自动运行命令

```gdscript
//devcontainer.json
{
...

  "postCreateCommand": "yarn install"

  // "remoteUser": "root"
}

```

# 配置启动容器的环境

```gdscript
{
    "name": "Java Development",
    "build": {
        "dockerfile": "./Dockerfile",
        "context": "."
    },
    "containerEnv": { # 配置环境变量
        "JAVA_HOME": "/usr/lib/jvm/java-21-amazon-corretto"
    }
}
```

‍

# 使用dockerfile 构建

**dev-container.json**

```gdscript
{
    "name": "Java Development",
    "build": {
        "dockerfile": "./Dockerfile",
        "context": "."
    },
    "features": {
        "ghcr.io/devcontainers/features/git:1": {
            "version": "latest",
            "ppa": "false"
        }
    },
    "containerEnv": { # 配置
        "JAVA_HOME": "/usr/lib/jvm/java-21-amazon-corretto"
    },
    "customizations": {
        "vscode": {
            "settings": {},
            "extensions": [
                "vscjava.vscode-java-pack"
            ]
        }
    },
    "remoteUser": "root"
}
```

```gdscript
FROM amazoncorretto:21 # 从指定的镜像构建
USER root # 指明是root 用户
ENV JAVA_HOME /usr/lib/jvm/java-21-amazon-corretto
ENV PATH "${JAVA_HOME}/bin:${PATH}"
```

‍

# 使用docker compose

对于单个项目

```gdscript
repository/
  - .devcontainer/
    - compose-devcontainer.yml
    - devcontainer.json
  - src/
  - compose.yml
```

对于其他的momorepo

```gdscript
repository/
  - frontend/
    - .devcontainer/
      - compose-devcontainer.yml
      - devcontainer.json
    - src/
  - backend/
    - .devcontainer/
      - compose-devcontainer.yml
      - devcontainer.json
    - src/
  - compose.yml
```

dev container 使用compose 作为启动

```
{
  "name": "frontend",
  "dockerComposeFile": [
    "../../compose.yml",
    "compose-devcontainer.yml"
  ],
  "service": "frontend",  # 待开发容器的Docker Compose上的服务名称
  "workspaceFolder": "/usr/src/app",
}
```

workspaceFolder：容器内部，VSCode打开的目录路径 应该是你在compose.yml中挂载源代码的路径、

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
