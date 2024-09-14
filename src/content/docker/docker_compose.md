---
title: docker compose
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Docker']
description: Docker学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/6ecf993c-71e8-11ef-96f2-ba1ea485754b.jpg
category: Docker
draft: false
---


# docker compose 

[Docker Compose - What is It, Example &amp; Tutorial (spacelift.io)](https://spacelift.io/blog/docker-compose)

在这篇文章中，我们将分享Compose的基础知识以及如何使用它。我们还将提供一些使用Compose部署流行应用程序的例子。让我们开始吧！

我们将涵盖以下内容：

1. [什么是Docker Compose](https://spacelift.io/blog/docker-compose#whatis-docker-compose)
2. [Docker Compose的好处](https://spacelift.io/blog/docker-compose#docker-compose-benefits)
3. [如何使用Docker Compose](https://spacelift.io/blog/docker-compose#tutorial-using-docker-compose)
4. [Docker Compose使用示例](https://spacelift.io/blog/docker-compose#docker-compose-examples)

## 什么是Docker Compose？

Docker Compose是一个工具，它使得创建和运行多容器应用程序变得更加容易。它自动化了同时管理多个Docker容器的过程，例如网站前端、API和数据库服务。

Docker Compose允许你在可以提交到源代码库的YAML文件中以代码的形式定义你的应用程序容器。一旦你创建了你的文件（通常命名为docker-compose.yml），你可以用一个Compose命令启动所有的容器（称为“服务”）。

与手动启动和链接容器相比，Compose更快、更容易、更可重复。你的容器每次都将以相同的配置运行——没有忘记包含重要的docker运行标志的风险。

Compose自动为你的项目创建一个[Docker网络](https://spacelift.io/blog/docker-networking)，确保你的容器可以相互通信。它还管理你的[Docker存储卷](https://spacelift.io/blog/docker-volumes)，在服务重新启动或替换后自动重新附加它们。

### 为什么使用Docker Compose？

大多数现实世界的应用程序都有多个具有依赖关系的服务——例如，你的应用程序可能在一个容器中运行，但依赖于在另一个相邻容器中部署的数据库服务器。此外，服务通常需要在部署前用存储卷、环境变量、端口绑定和其他设置进行配置。

Compose让你将这些需求封装为特定于你的应用程序的“堆栈”容器。使用Compose启动堆栈会使用你在文件中设置的配置值启动每个容器。这提高了开发者的人体工程学，支持在多个环境中重用堆栈，并有助于防止意外的配置错误。

### Docker和Docker Compose之间的区别是什么？

[Docker](https://spacelift.io/blog/docker-tutorial) 是一个容器化引擎，它提供了一个用于在主机上构建、运行和管理单个容器的CLI。

Compose是一个扩展Docker以支持多容器管理的工具。它支持在项目级配置文件中声明性定义的容器“堆栈”。

你可以在没有Compose的情况下使用Docker；然而，当你开发一个容器化系统时，采用Compose允许你用一个命令在任何环境中部署你的应用程序。而Docker CLI一次只与一个容器交互，Compose与你的项目集成，并了解你的容器之间的关系。

## Docker Compose的好处

以下是使用Docker Compose的一些好处：

* 使用YAML脚本快速且容易配置
* 单主机部署
* 提高生产力
* 通过隔离容器提高安全性

## 教程：如何使用Docker Compose

让我们看看如何在你自己的应用程序中开始使用Compose。我们将创建一个简单的Node.js应用程序，它需要连接到在另一个容器中运行的Redis服务器。

### 1. 检查是否安装了Docker Compose

从历史上看，Docker Compose作为名为`docker-compose`​的独立二进制文件分发，与Docker Engine分开。自从[Compose v2推出](https://docs.docker.com/compose/migrate)以来，该命令现在已内置于`docker`​ CLI中作为`docker compose`​。不再支持Compose v1。

如果你使用的是Docker Desktop或Docker Engine的现代版本，你应该已经可以使用Docker Compose v2了。你可以通过运行`docker compose version`​命令来检查：

```bash
$ docker compose version
Docker Compose version v2.18.1
```

### 2. 创建你的应用程序

通过复制以下代码并将其保存到工作目录中的`app.js`​来开始本教程：

```js
const express = require("express");
const {createClient: createRedisClient} = require("redis");

(async function () {

    const app = express();

    const redisClient = createRedisClient({
        url: `redis://redis:6379`
    });

    await redisClient.connect();

    app.get("/", async (request, response) => {
        const counterValue = await redisClient.get("counter");
        const newCounterValue = ((parseInt(counterValue) || 0) + 1);
        await redisClient.set("counter", newCounterValue);
        response.send(`Page loads: ${newCounterValue}`);
    });

    app.listen(80);

})();
```

代码使用了[Express](https://expressjs.com/) 网络服务器包来创建一个简单的点击跟踪应用程序。每次你访问应用程序时，它都会在Redis中记录你的点击次数，然后显示页面加载的总次数。

使用npm安装应用程序的依赖项：

```hcl
$ npm install express redis

```

接下来，将以下Dockerfile内容复制到工作目录中的Dockerfile：

```bash
FROM node:18-alpine

EXPOSE 80
WORKDIR /app

COPY package.json .
COPY package-lock.json .
RUN npm install

COPY app.js .

ENTRYPOINT ["node", "app.js"]
```

稍后Compose将构建这个Dockerfile以创建你的应用程序的Docker镜像。

### 3. 创建一个Docker Compose文件

现在，你已经准备好将Compose添加到你的项目中了。这个应用程序非常适合使用Compose，因为你需要两个容器来成功运行应用程序：

1. **容器1 – 你创建的Node.js服务器应用程序。**
2. **容器2 – 你的Node.js应用程序要连接的Redis实例。**

创建一个`docker-compose.yml`​文件是使用Compose的第一步。复制以下内容并将其保存到你自己的`docker-compose.yml`​中——不用担心，我们将在下面解释：

```yaml
services:
  app:
    image: app:latest
    build:
      context: .
    ports:
      - ${APP_PORT:-80}:80
  redis:
    image: redis:6
```

让我们深入了解这里发生了什么。

1. 顶级字段是你定义应用程序所需的容器的地方。
2. 这个应用程序指定了两个服务：`app`​（你的Node.js应用程序）和`redis`​（你的Redis服务器）。
3. 每个服务都有一个`image`​字段，定义了容器将运行的Docker镜像。在应用程序服务的情况下，它是自定义的`app:latest`​镜像。由于这个镜像可能尚不存在，因此设置了字段，告诉Compose可以使用工作目录（`.`​）作为[构建上下文](https://docs.docker.com/build/building/context)来构建镜像。`redis`​服务更简单，它只需要引用Docker Hub上的[官方Redis镜像](https://hub.docker.com/_/redis)。
4. ​`app`​服务有一个`ports`​字段，声明了要应用到容器的端口绑定，类似于`docker run`​的标志。使用了[插值变量](https://docs.docker.com/compose/compose-file/12-interpolation)；这意味着当你设置了`APP_PORT`​环境变量时，将提供端口号，如果没有设置，则默认回退到端口80。

从这个解释中，你可以看到Compose文件包含了启动应用程序所需的所有配置。

### 4. 启动你的容器

现在，你可以使用Compose来启动堆栈了！

调用`docker compose up`​来启动你的`docker-compose.yml`​文件中的所有服务。和调用`docker run`​时一样，你应该添加`-d`​参数来分离你的终端并在后台运行服务：

```bash
$ docker compose up -d
[+] Building 0.5s (11/11) FINISHED
...
[+] Running 3/3
 ✔ Network node-redis_default    Created  0.1s 
 ✔ Container node-redis-redis-1  Started  0.7s 
 ✔ Container node-redis-app-1    Started  0.6s 
```

由于你的应用程序镜像尚不存在，Compose将首先从你的Dockerfile构建它。然后它将通过创建一个Docker网络并启动你的容器来运行你的堆栈。

在浏览器中访问localhost，看看你的应用程序在行动。

​![install docker compose]()​

尝试几次刷新页面——你会看到每次点击都被记录在Redis中，并且计数器会增加。

​![docker compose file]()​

在`app.js`​文件中，我们将Redis客户端URL设置为`redis:6379`​。`redis`​主机名与`docker-compose.yml`​中的`redis`​服务名称匹配。

Compose使用你的服务名称来分配你的容器主机名；因为容器是同一Docker网络的一部分，你的应用程序容器可以将`redis`​主机名解析为你的Redis实例。

### 5. 管理你的Docker Compose堆栈 – 命令

既然你已经启动了你的应用程序，你可以使用其他Docker Compose命令来管理你的堆栈：

#### docker compose ps

你可以通过运行`ps`​命令来查看Compose创建的容器；输出与`docker ps`​产生的输出匹配：

```bash
$ docker compose ps
NAME                 IMAGE               COMMAND                  SERVICE             CREATED             STATUS              PORTS
node-redis-app-1     app:latest          "node app.js"            app                 12 minutes ago      Up 12 minutes       0.0.0.0:80->80/tcp, :::80->80/tcp
node-redis-redis-1   redis:6             "docker-entrypoint.s…"   redis               12 minutes ago      Up 12 minutes       6379/tcp
```

#### docker compose stop

此命令将[停止由堆栈创建的所有Docker容器](https://spacelift.io/blog/docker-stop-container)。之后使用`docker compose start`​重新启动它们。

#### docker compose restart

​`restart`​命令会立即强制重启你的堆栈容器。

#### docker compose down

使用此命令来移除由`docker compose up`​创建的对象。它将销毁你的堆栈容器和网络。

除非你设置了`-v`​或`--volumes`​标志，否则**不会**删除卷。这可以防止意外丢失持久数据。

#### docker compose logs

使用`logs`​命令查看你的堆栈容器的输出。这会收集堆栈中所有容器的标准输出和错误流。每一行日志都标记了创建它的容器的名称。

#### docker compose build

你可以使用`build`​命令强制重建你的镜像。这将重建`docker-compose.yml`​文件中包含`build`​字段的服务的镜像。

之后，你可以重复`docker compose up`​命令，用重建的镜像重新启动你的堆栈。

#### docker compose push

构建镜像后，使用`push`​将它们全部推送到远程仓库URL。同样，`docker compose pull`​将检索堆栈所需的镜像，而不会启动任何容器。

### 6. 使用Compose配置文件

有时，你的堆栈中的服务可能是可选的。例如，你可以扩展演示应用程序以支持使用Redis之外的替代数据库引擎。当使用不同的引擎时，你就不需要Redis容器了。

你可以使用Compose的[配置文件功能](https://docs.docker.com/compose/profiles)来适应这些需求。将服务分配给配置文件允许你在运行Compose命令时手动激活它们：

```yaml
services:
  app:
    image: app:latest
    build:
      context: .
    ports:
      - ${APP_PORT:-80}:80
  redis:
    image: redis:6
    profiles:
      - with-redis
```

这个docker-compose.yml文件将redis服务分配给一个名为with-redis的配置文件。现在，只有在你的docker compose命令中包含--profile with-redis标志时，才会考虑Redis容器：  
  

```bash
# Does not start Redis
$ docker compose up -d

# Will start Redis
$ docker compose --profile with-redis up -d
```

### 7. 理解Docker Compose项目

项目是Docker Compose v2中的一个重要概念。你的“项目”是你的`docker-compose.yml`​文件以及它创建的资源。

Compose默认使用你的工作目录中的`docker-compose.yml`​文件。它假设你的项目名称等于你的工作目录的名称。此名称为Compose创建的Docker对象（例如你的容器和网络）添加前缀。你可以通过设置Compose的`--project-name`​标志或在`docker-compose.yml`​文件中包含顶级`name`​字段来覆盖项目名称：

```bash
name: "demo-app"
services:
  ...
```

你可以通过设置--profile-directory标志从项目的工作目录外部运行Docker Compose命令：

```bash
$ docker compose --profile-directory=/path/to/directory ps
```

该标志接受一个docker-compose.yml文件的路径，或包含一个的目录。

### 8. 设置Docker Compose环境变量

Docker Compose的一个优点是你可以轻松地为服务设置环境变量。

而不是手动重复`docker run -e`​标志，你可以在你的`docker-compose.yml`​文件中[定义变量](https://docs.docker.com/compose/environment-variables/set-environment-variables)，设置默认值，并促进简单的覆盖：

```yaml
services:
  app:
    image: app:latest
    build:
      context: .
    environment:
      - DEV_MODE
      - REDIS_ENABLED=1
      - REDIS_HOST_URL=${REDIS_HOST:-redis}
    ports:
      - ${APP_PORT:-80}:80
```

这个例子展示了几种不同的设置变量的方法：

* ​**​`DEV_MODE`​**​ – 不提供值意味着Compose将从你在shell中设置的环境变量中获取它。
* ​**​`REDIS_ENABLED=1`​**​ – 设置一个特定值将确保使用它（除非后来被覆盖）。
* ​**​`REDIS_HOST_URL=${REDIS_HOST:-redis}`​** ​ – 这个插值示例将`REDIS_HOST_URL`​分配给你的`REDIS_HOST`​ shell变量的值，回退到默认值`redis`​。
* ​ **​`${APP_PORT:-80}`​** ​ – 在你的shell中设置的环境变量可以被插值到你的`docker-compose.yml`​文件中的任意字段，允许轻松自定义你的堆栈配置。

此外，你可以通过创建一个环境文件来覆盖这些值——要么是.env（自动加载），要么是你传递给Compose的--env-file标志的另一个文件：

```bash
$ cat config.env
DEV_MODE=1
APP_PORT=8000

$ docker compose --env-file=config.env up -d
```

### 9. 控制服务启动顺序

许多应用程序要求它们的组件等待依赖项准备就绪——例如，在我们上面的演示应用程序中，如果Node应用程序在Redis容器启动之前启动，它将会崩溃。

你可以通过在`docker-compose.yml`​文件中设置`depends_on`​字段来控制服务启动的顺序：

```yaml
services:
  app:
    image: app:latest
    build:
      context: .
    depends_on:
      - redis
    ports:
      - ${APP_PORT:-80}:80
  redis:
    image: redis:6
```

现在，Compose将延迟启动app服务，直到redis容器正在运行。为了更大的安全性，你可以等待容器通过其健康检查，使用depends_on的长格式代替：

```yaml
services:
  app:
    image: app:latest
    build:
      context: .
    depends_on:
      redis:
        condition: service_healthy
    ports:
      - ${APP_PORT:-80}:80
  redis:
    image: redis:6

```

## Docker Compose示例

你想看到Compose在部署一些现实世界应用程序中的实际操作吗？这里有一些例子！

### WordPress（Apache/PHP和MySQL）与Docker Compose

WordPress是最受欢迎的网站内容管理系统（CMS）。它是一个PHP应用程序，需要连接MySQL或MariaDB数据库。因此，有需要用Docker部署的两个容器：

1. **WordPress应用程序容器** – 使用PHP和Apache网络服务器提供WordPress。
2. **MySQL数据库容器** – 运行WordPress容器将连接的数据库服务器。

以下`docker-compose.yml`​文件可以用来创建这些容器并启动一个功能齐全的WordPress网站：

```yaml
services:
  wordpress:
    image: wordpress:${WORDPRESS_TAG:-6.2}
    depends_on:
      - mysql
    ports:
      - ${WORDPRESS_PORT:-80}:80
    environment:
      - WORDPRESS_DB_HOST=mysql
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=${DATABASE_USER_PASSWORD}
      - WORDPRESS_DB_NAME=wordpress
    volumes:
      - wordpress:/var/www/html
    restart: unless-stopped
  mysql:
    image: mysql:8.0
    environment:
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=${DATABASE_USER_PASSWORD}
      - MYSQL_RANDOM_ROOT_PASSWORD="1"
    volumes:
      - mysql:/var/lib/mysql
    restart: unless-stopped

volumes:
  wordpress:
  mysql:
```

这个Compose文件包含了配置连接到MySQL数据库的WordPress部署所需的一切。

[[Docker卷](https://spacelift.io/blog/docker-volumes)](也定义了，用于存储容器创建的持久数据，独立于它们的容器生命周期。  
现在你可以用一个简单的命令启动MySQL——唯一需要的环境变量是`wordpress`​数据库用户的​密码：

```bash
$ DATABASE_USER_PASSWORD=abc123 docker compose up -d
```

在浏览器中访问localhost，进入你的WordPress网站安装页面：

​![docker-compose]()​

### 

### Prometheus和Grafana与Docker Compose

[Prometheus](https://spacelift.io/blog/prometheus-kubernetes)是一个流行的时间序列数据库，用于从应用程序收集指标。它通常与[Grafana](https://grafana.com/)配对，Grafana是一个可观测平台，允许将来自Prometheus和其他来源的数据可视化在图形仪表板上。

让我们使用Docker Compose部署并连接这些应用程序。

首先，创建一个Prometheus配置文件——这配置了应用程序来抓取自己的指标，为我们演示目的提供数据：

```yaml
scrape_configs:
- job_name: prometheus
  honor_timestamps: true
  scrape_interval: 10s
  scrape_timeout: 5s
  metrics_path: /metrics
  scheme: http
  static_configs:
  - targets:
    - localhost:9090
```

将文件保存到工作目录中的`prometheus/prometheus.yml`​。

接下来，创建一个Grafana文件，它将配置应用程序与你的Prometheus实例的数据源连接：

```yaml
apiVersion: 1

datasources:
- name: Prometheus
  type: prometheus
  url: http://prometheus:9090
  access: proxy
  isDefault: true
  editable: true
This file should be saved to grafana/grafana.yml in your working directory.
Finally, copy the following Compose file and save it to docker-compose.yml:
services:
  prometheus:
    image: prom/prometheus:latest
    command:
      - "--config.file=/etc/prometheus/prometheus.yml"
    ports:
      - 9090:9090
    volumes:
      - ./prometheus:/etc/prometheus
      - prometheus:/prometheus
    restart: unless-stopped
  grafana:
    image: grafana/grafana:latest
    ports:
      - ${GRAFANA_PORT:-3000}:3000
    environment:
      - GF_SECURITY_ADMIN_USER=${GRAFANA_USER:-admin}
      - GF_SECURITY_ADMIN_PASSWORD=${GRAFANA_PASSWORD:-grafana}
    volumes:
      - ./grafana:/etc/grafana/provisioning/datasources
    restart: unless-stopped
volumes:
  prometheus:
```

使用docker compose up启动服务，并可选地为你的Grafana帐户设置自定义用户凭据：

```bash
$ GRAFANA_USER=demo GRAFANA_PASSWORD=foobar docker compose up -d
```

现在在浏览器中访问localhost:3000登录Grafana：

​![docker compose grafana]()​

## 

## 关键点

在这篇文章中，你已经学会了如何使用Docker Compose来处理多个Docker容器的堆栈。我们已经展示了如何创建一个Compose文件，并看了一些WordPress和Prometheus/Grafana的例子。

现在你可以使用Compose与你的应用程序容器交互，同时避免使用错误倾向的`docker run`​ CLI命令。一个`docker compose up`​将启动你堆栈中的所有容器，确保在任何环境中都有一致的配置。

你也可以看看[Spacelift](https://spacelift.io/)如何使用Docker容器来[运行CI作业](https://docs.spacelift.io/integrations/docker)。Spacelift在自定义工作流方面提供了完全的灵活性。你可以自带Docker镜像，并[将其作为运行器](https://docs.spacelift.io/integrations/docker)来加速部署，利用第三方工具。

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
