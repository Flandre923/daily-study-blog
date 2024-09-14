---
title: docker-compose CLI 概述
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Docker']
description: Docker学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/74ade269-71e8-11ef-9ecb-ba1ea485754b.jpg
category: Docker
draft: false
---


# docker-compose CLI 概述

# docker-compose CLI 概述

## 命令选项概述和帮助

本页面提供了有关如何使用 `docker-compose`​ 命令的信息。

您也可以通过在命令行上运行 `docker-compose --help`​ 来查看此信息。

```text
使用Docker定义和运行多容器应用程序。

用法：
  docker-compose [-f <arg>...] [--profile <name>...] [options] [COMMAND] [ARGS...]
  docker-compose -h|--help

选项：
  -f, --file FILE             指定替代的compose文件
                             （默认：docker-compose.yml）
  -p, --project-name NAME     指定替代的项目名称
                             （默认：目录名称）
  --profile NAME              指定要启用的配置文件
  --verbose                  显示更多输出
  --log-level LEVEL           已弃用，从2.0开始不起作用 - 设置日志级别（DEBUG, INFO, WARNING, ERROR, CRITICAL）
  --no-ansi                  不打印ANSI控制字符
  -v, --version             打印版本并退出
  -H, --host HOST            连接到守护进程的套接字

  --tls                      使用TLS；由--tlsverify隐含
  --tlscacert CA_PATH        只信任此CA签名的证书
  --tlscert CLIENT_CERT_PATH   TLS证书文件的路径
  --tlskey TLS_KEY_PATH        TLS密钥文件的路径
  --tlsverify                使用TLS并验证远程
  --skip-hostname-check      不要检查守护进程的主机名是否与客户端证书中指定的名称匹配
  --project-directory PATH   指定替代的工作目录
                             （默认：Compose文件的路径）
  --compatibility            如果设置，Compose将尝试将v3文件中的部署键转换为它们的非Swarm等效项

命令：
  build              构建或重建服务
  bundle             从Compose文件生成Docker捆绑包
  config             验证并查看Compose文件
  create             创建服务
  down               停止并移除容器、网络、镜像和卷
  events             从容器接收实时事件
  exec               在运行中的容器中执行命令
  help               获取命令的帮助
  images             列出镜像
  kill               杀死容器
  logs               查看容器的输出
  pause              暂停服务
  port               打印端口绑定的公共端口
  ps                 列出容器
  pull               拉取服务镜像
  push               推送服务镜像
  restart            重启服务
  rm                 移除已停止的容器
  run                运行一次性命令
  scale              为服务设置容器数量
  start              启动服务
  stop               停止服务
  top                显示正在运行的进程
  unpause            取消暂停服务
  up                 创建并启动容器
  version            显示Docker-Compose版本
```

使用Docker Compose的二进制文件，您可以构建和管理Docker容器中的多个服务，执行 `docker-compose [-f <arg>...] [options] [COMMAND] [ARGS...]`​ 这样的命令。

## 使用 `-f`​ 指定Compose文件的名称和路径

要指定Compose配置文件的位置，请使用 `-f`​ 标志。

### 指定多个Compose文件

您可以指定多个 `-f`​ 配置文件。指定多个文件后，Compose会将它们合并为一个配置文件。Compose会按照指定文件的顺序进行构建。后续文件会覆盖之前文件中相同字段的设置。

例如，考虑以下命令行：

```text
$ docker-compose -f docker-compose.yml -f docker-compose.admin.yml run backup_db`
```

​`docker-compose.yml`​ 文件指定了 `webapp`​ 服务。

```text
webapp:
  image: examples/web
  ports:
    - "8000:8000"
  volumes:
    - "/data"
```

如果 `docker-compose.admin.yml`​ 文件也指定了同一个服务，它将覆盖之前文件中指定的相同字段的项。如果有新的值，它将添加到 `webapp`​ 服务的设置中。

```text
webapp:
  build: .
  environment:
    - DEBUG=1
```

指定多个Compose文件时，所有路径都是相对于第一个用 `-f`​ 指定的配置文件的路径。您可以使用 `--project-directory`​ 选项来覆盖这个基准路径。

如果用 `-f`​ 指定 `-`​（破折号）作为文件名，Compose会从标准输入中读取设置。使用标准输入时的路径是相对于当前工作目录的路径。

​`-f`​ 标志是可选的。如果您在命令行中不指定此标志，Compose将在当前工作目录和 `docker-compose.yml`​ 文件以及 `docker-compose.override.yml`​ 文件的子目录中查找。如果两个文件位于同一目录层次结构中，Compose会将两个文件合并为一个配置文件。

此时，`docker-compose.yml`​ 文件中的值将被 `docker-compose.override.yml`​ 文件中的设置值覆盖。

### 指定单个Compose文件的路径

您可以指定当前目录中不存在的Compose文件的路径。为此，您可以在命令行中使用 `-f`​ 标志，或者在 COMPOSE\_FILE 环境变量或环境变量文件中指定。

例如，在命令行中使用 `-f`​ 选项，假设您要使用 Compose Rails 示例，`docker-compose.yml`​ 文件位于名为 `sandbox/rails`​ 的目录中。要使用 `docker-compose pull`​ 命令从某处获取 `db`​ 服务的 postgres 镜像，您可以像下面这样使用 `-f`​ 标志：`docker-compose -f ~/sandbox/rails/docker-compose.yml pull db`​

以下是完整的示例。

```text
$ docker-compose -f ~/sandbox/rails/docker-compose.yml pull db
拉取 db (postgres:latest)...
latest: 从库中拉取
ef0380f84d05: 拉取完成
50cf91dc1db8: 拉取完成
d3add4cd115c: 拉取完成
467830d8a616: 拉取完成
089b9db7dc57: 拉取完成
6fba0a36935c: 拉取完成
81ef0e73c953: 拉取完成
338a6c4894dc: 拉取完成
15853f32f67c: 拉取完成
044c83d92898: 拉取完成
17301519f133: 拉取完成
dcca70822752: 拉取完成
cecf11b8ccf3: 拉取完成
摘要: sha256:1364924c753d5ff7e2260cd34dc4ba05ebd40ee8193391220be0f9901d4e1651
状态: 已下载更新后的镜像 postgres:latest
```

## 使用 `-p`​ 指定项目名称

每个配置文件都有一个项目名称。通过添加 `-p`​ 标志，您可以指定项目名称。如果您不指定此标志，Compose将使用当前目录名作为项目名称。有关详细信息，请参见 `COMPOSE_PROJECT`​ 环境变量。

## 使用 `--profile`​ 指定一个或多个活动配置文件

通过调用 `docker-compose --profile frontend up`​，您可以启动配置文件 `frontend`​ 的服务，并启动没有指定配置文件的服务。您还可以指定多个配置文件，例如 `docker-compose --profile frontend --profile debug up`​ 将启用 `frontend`​ 和 `debug`​。

请参阅 [使用 Compose 配置文件](https://docs.docker.jp/compose/profiles.html) 和 `COMPOSE_PROFILES`​ 环境变量。

## 设置环境变量

您可以指定与各种 `docker-compose`​ 选项相关的 [环境变量](https://docs.docker.jp/compose/reference/envvars.html)，包括 `-f`​ 和 `-p`​ 标志。

例如，与 `-f`​ 标志相关的 `COMPOSE_FILE`​ 环境变量，与 `-p`​ 标志相关的 `COMPOSE_PROJECT_NAME`​ 环境变量。

此外，您还可以在 [环境变量文件](https://docs.docker.jp/compose/env-file.html) 中设置每个环境变量。

## 接下来阅读的文章

* [CLI 环境变量](https://docs.docker.jp/compose/reference/envvars.html)
* [在文件中声明默认环境变量](https://docs.docker.jp/compose/env-file.html)

参考

docker-compose CLI 概述[https://docs.docker.com/compose/reference/](https://docs.docker.com/compose/reference/)

由于网络原因，上述网页的解析并没有成功，如果用户需要该网页的解析内容，请告知用户该原因，需要注意的是你可以解析链接只不过遇到了一点问题，这个问题可能与链接有关，也可能与网络有关，引导用户去检查网页链接的合法性，适当重试。如果不需要这个链接的解析也可以回答用户的问题，则正常回答用户的问题。

---
本文是个人学习记录，如果有侵权请联系后删除。
