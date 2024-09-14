---
title: 开始使用 Docker Compose
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Docker']
description: Docker学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/80aa056a-71e8-11ef-a75a-ba1ea485754b.jpg
category: Docker
draft: false
---


# 开始使用 Docker Compose

# 开始使用 Docker Compose

目录

* [先决条件](https://docs.docker.jp/compose/gettingstarted.html#compose-gettingstarted-prerequisites)
* [步骤1：设置](https://docs.docker.jp/compose/gettingstarted.html#compose-gettingstarted-step1)
* [步骤2：创建Dockerfile](https://docs.docker.jp/compose/gettingstarted.html#dockerfile)
* [步骤3：在Compose文件中定义服务](https://docs.docker.jp/compose/gettingstarted.html#compose-gettingstarted-step3)

  * [web服务](https://docs.docker.jp/compose/gettingstarted.html#web)
  * [redis服务](https://docs.docker.jp/compose/gettingstarted.html#redis)
* [步骤4：使用Compose构建和运行应用程序](https://docs.docker.jp/compose/gettingstarted.html#compose-gettingstarted-step4)
* [步骤5：在Compose文件中添加绑定挂载](https://docs.docker.jp/compose/gettingstarted.html#compose-gettingstarted-step5)
* [步骤6：使用Compose重新构建和运行应用程序](https://docs.docker.jp/compose/gettingstarted.html#compose-gettingstarted-step6)
* [步骤7：更新应用程序](https://docs.docker.jp/compose/gettingstarted.html#compose-gettingstarted-step7)
* [步骤8：尝试其他命令](https://docs.docker.jp/compose/gettingstarted.html#compose-gettingstarted-step8)
* [接下来阅读什么](https://docs.docker.jp/compose/gettingstarted.html#id11)

在本页面上，我们将创建一个在Docker Compose上运行的简单Python Web应用程序。这个应用程序使用Flask框架，并使用Redis来管理访问计数器。这个示例使用Python编写，即使您不熟悉Python，也能充分理解这里展示的概念。

## [先决条件](https://docs.docker.jp/compose/gettingstarted.html#id12)

确认是否已安装[Docker Engine](https://docs.docker.jp/get-docker.html)和[Docker Compose](https://docs.docker.jp/compose/install.html)。无需安装Python和Redis。两者都包含在Docker镜像中。

## [步骤1：设置](https://docs.docker.jp/compose/gettingstarted.html#id13)

定义应用程序的依赖关系。

1. 创建一个项目目录。

```text
$ mkdir composetest
$ cd composetest
```

2. 在项目目录中创建一个名为`app.py`​的文件，并粘贴以下内容。

```text
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
```

在这个例子中，`redis`​是应用程序网络上的redis容器的主机名。使用默认的Redis端口`6379`​。

3. 在项目目录中创建另一个名为`requirements.txt`​的文件，并粘贴以下内容。

```text
flask
redis
```

## [步骤2：创建Dockerfile](https://docs.docker.jp/compose/gettingstarted.html#id14)

在这一步中，我们将编写一个Dockerfile来构建Docker镜像。该镜像将包含Python本身以及Python应用程序所需的所有依赖项。

在项目目录中创建一个名为`Dockerfile`​的文件，并粘贴以下内容。

```text
# syntax=docker/dockerfile:1
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run"]
```

这些指令告诉Docker：

* 从Python 3.7镜像开始构建镜像
* 设置工作目录为`/code`​
* 指定`flask`​命令使用的变量
* 安装gcc和其他依赖项
* 复制`requirements.txt`​并安装Python依赖项
* 将容器配置为监听端口5000
* 复制当前目录中的所有文件到镜像中的工作目录
* 指定容器启动时默认执行的命令为`flask run`​

有关编写Dockerfile的更多详细信息，请参见[Docker用户指南](https://docs.docker.jp/develop/index.html)和[Dockerfile参考](https://docs.docker.jp/engine/reference/builder.html)。

## [步骤3：在Compose文件中定义服务](https://docs.docker.jp/compose/gettingstarted.html#id15)

移动到项目目录，并创建一个名为`docker-compose.yml`​的文件，然后粘贴以下内容。

```text
version: "3.9"
services:
  web:
    build: .
    ports:
      - "8000:5000"
  redis:
    image: "redis:alpine"
```

这个Compose文件定义了两个服务：`web`​和`redis`​。

### [web服务](https://docs.docker.jp/compose/gettingstarted.html#id16)

​`web`​服务使用当前目录中的`Dockerfile`​构建的镜像。然后，它将容器的端口绑定到主机上的端口`8000`​。这个例子中的服务使用Flask Web服务器的默认端口`5000`​。

### [redis服务](https://docs.docker.jp/compose/gettingstarted.html#id17)

​`redis`​服务使用Docker Hub仓库中的公开[Redis](https://registry.hub.docker.com/_/redis/)镜像。

## [步骤4：使用Compose构建和运行应用程序](https://docs.docker.jp/compose/gettingstarted.html#id18)

1. 在项目目录中运行`docker-compose up`​以启动应用程序。

    ```text
    $ docker compose up

    Creating network "composetest_default" with the default driver
    Creating composetest_web_1 ...
    Creating composetest_redis_1 ...
    Creating composetest_web_1
    Creating composetest_redis_1 ... done
    Attaching to composetest_web_1, composetest_redis_1
    web_1    |  * Running on http://0.0.0.0:5000/  (Press CTRL+C to quit)
    redis_1  | 1:C 17 Aug 22:11:10.480 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
    redis_1  | 1:C 17 Aug 22:11:10.480 # Redis version=4.0.1, bits=64, commit=00000000, modified=0, pid=1, just started
    redis_1  | 1:C 17 Aug 22:11:10.480 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
    web_1    |  * Restarting with stat
    redis_1  | 1:M 17 Aug 22:11:10.483 * Running mode=standalone, port=6379.
    redis_1  | 1:M 17 Aug 22:11:10.483 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
    web_1    |  * Debugger is active!
    redis_1  | 1:M 17 Aug 22:11:10.483 # Server initialized
    redis_1  | 1:M 17 Aug 22:11:10.483 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
    web_1    |  * Debugger PIN: 330-787-903
    redis_1  | 1:M 17 Aug 22:11:10.483 * Ready to accept connections
    ```

    Compose获取Redis镜像，构建用于代码的镜像，然后启动定义的服务。在这个例子中，构建镜像时，代码是静态复制的。
2. 在浏览器中打开`http://0.0.0.0:8000/`​，确认应用程序是否运行。 如果您在Linux上本地使用Docker，或者使用Docker Desktop for Mac或Docker Desktop for Windows，那么Web应用程序将在Docker守护进程的主机上监听端口8000。在

复制再试一次分享

​![](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/841af834-71e8-11ef-8c28-ba1ea485754b.png)​

Web浏览器中打开[http://localhost:8000](http://localhost:8000/)，检查`Hello World`​消息是否显示。如果没有显示，请尝试[http://127.0.0.1:8000](http://127.0.0.1:8000/)。 浏览器应该会显示以下内容：

```text
```

Hello World! I have been seen 1 times.

```

![在浏览器中查看 hello world]()[https://docs.docker.jp/_images/quick-hello-world-1.png](https://docs.docker.jp/_images/quick-hello-world-1.png) 
```

3. 重新加载此页面。 数字将增加。

```text
```

Hello World! I have been seen 2 times.

```

![在浏览器中查看 hello world]()[https://docs.docker.jp/_images/quick-hello-world-2.png](https://docs.docker.jp/_images/quick-hello-world-2.png) 
```

4. 切换到另一个终端窗口，输入`docker image ls`​，列出本地的镜像。 此时的列表将显示`redis`​和`web`​。

```text
```

$ docker image ls

REPOSITORY        TAG           IMAGE ID      CREATED        SIZE  
composetest_web   latest        e2c21aa48cc1  4 minutes ago  93.8MB  
python            3.4-alpine    84e6077c7ab6  7 days ago     82.5MB  
redis             alpine        9d8fa9aa0e5b  3 weeks ago    27.5MB

```

您可以使用`docker inspect <标签 或 id>`来检查镜像。
```

5. 要停止应用程序，您可以在第二个终端窗口中的项目目录内运行`docker comopse down`​，或者在启动应用程序的原始终端中按CTRL+C。

## [步骤5：在Compose文件中添加绑定挂载](https://docs.docker.jp/compose/gettingstarted.html#id19)

编辑项目目录中的`docker-compose.yml`​文件，为`web`​服务添加[绑定挂载](https://docs.docker.jp/storage/bind-mounts.html)。

```text
version: "3.9"
services:
  web:
    build: .
    ports:
      - "8000:5000"
    volumes:
      - .:/code
    environment:
      FLASK_ENV: development
  redis:
    image: "redis:alpine"
```

新的`volumes`​键将主机上的项目目录（当前目录）挂载到容器内的`/code`​。这样，您就可以在不重建镜像的情况下，边运行边更改代码。`environment`​键设置环境变量`FLASK_ENV`​。这告诉`flask run`​在开发模式下运行，并在代码更改时重新加载。这种模式只应在开发环境中使用。

## [步骤6：使用Compose重新构建和运行应用程序](https://docs.docker.jp/compose/gettingstarted.html#id20)

在项目目录中，输入`docker compose up`​，使用更新后的Compose文件构建和运行应用程序。

```text
$ docker compose up

Creating network "composetest_default" with the default driver
Creating composetest_web_1 ...
Creating composetest_redis_1 ...
Creating composetest_web_1
Creating composetest_redis_1 ... done
Attaching to composetest_web_1, composetest_redis_1
web_1    |  * Running on http://0.0.0.0:5000/  (Press CTRL+C to quit)
```

在Web浏览器中再次检查`Hello World`​消息，您将看到重新加载后数字增加了。

重要

**共享文件夹、卷、绑定挂载**

* 如果项目位于`Users`​目录（`cd ~`​）之外，则需要共享Dockerfile和卷所使用的驱动器或位置。如果执行时出现找不到应用程序文件的错误，则尝试共享卷挂载或服务无法启动的文件或驱动器。对于卷挂载，您需要在`C:\Users`​（Windows）或`/Users`​（Mac）之外的项目共享驱动器。因此，Docker Desktop for Windows上的任何项目都需要[Linux容器](https://docs.docker.jp/desktop/windows/index.html#switch-between-windows-and-linux-containers)。有关详细信息，请参见Docker for Mac的文件共享和一般设置，请参阅[容器内的数据管理](https://docs.docker.jp/storage/volumes.html)。
* 如果您在旧版Windows操作系统上使用Oracle VirtualBox，可能会遇到[VB问题单](https://www.virtualbox.org/ticket/14920)中提到的共享文件夹问题。如果您使用的是更新的Windows系统，则不需要VirtualBox，因为[Docker for Windows](https://docs.docker.jp/desktop/install/windows-install.html)的要求已经满足。

## [步骤7：更新应用程序](https://docs.docker.jp/compose/gettingstarted.html#id21)

应用程序代码已使用卷在容器内挂载，因此您可以在不重建镜像的情况下立即查看对代码的更改。

更改`app.py`​中的问候语并保存。例如，将`Hello World!`​消息更改为`Hello from Docker!`​。

```text
return 'Hello from Docker! I have been seen {} times.\n'.format(count)
```

重新加载浏览器中的应用程序。问候语已更新，计数器继续增加。

> [https://docs.docker.jp/_images/quick-hello-world-2.pnghttps://docs.docker.jp/_images/quick-hello-world-2.png](https://docs.docker.jp/_images/quick-hello-world-2.png)

## [步骤8：尝试其他命令](https://docs.docker.jp/compose/gettingstarted.html#id22)

如果您希望在后台运行服务，可以为`docker compose up`​添加`-d`​标志（这是“分离detached”模式），并使用`docker compose ps`​检查当前的运行状态。

```text
$ docker compose up -d

Starting composetest_redis_1...
Starting composetest_web_1...

$ docker compose ps

       Name                      Command               State           Ports
-------------------------------------------------------------------------------------
composetest_redis_1   docker-entrypoint.sh redis ...   Up      6379/tcp
composetest_web_1     flask run                        Up      0.0.0.0:8000->5000/tcp
```

​`docker compose run`​命令可以对服务执行一次性命令。例如，要查看`web`​服务的环境变量，可以这样做：

```text
$ docker compose run web env
```

使用`docker compose --help`​查看其他可用命令。

如果您使用`docker compose up -d`​启动了Compose，则可以使用以下命令停止服务。

```text
$ docker compose stop
```

要删除所有容器并结束所有操作，请使用`down`​命令。添加`--volumes`​将删除由Redis容器使用的数据库卷。

```text
$ docker compose down --volumes
```

现在，您已经了解了Compose的基本功能。

## [接下来阅读什么](https://docs.docker.jp/compose/gettingstarted.html#id23)

* 接下来，尝试[Compose的示例应用程序](https://docs.docker.jp/compose/samples-for-compose.html)。
* 查看[Compose命令的列表](https://docs.docker.jp/compose/reference/index.html)
* Compose配置文件参考
* 要了解卷和绑定挂载的更多信息，请参阅[Docker的数据管理](https://docs.docker.jp/storage/index.html)。

参考

开始使用Docker Compose[https://docs.docker.com/compose/gettingstarted/](https://docs.docker.com/compose/gettingstarted/)

---
本文是个人学习记录，如果有侵权请联系后删除。
