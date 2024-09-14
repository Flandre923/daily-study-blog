---
title: Introduction to Docker Compose  Baeldung on Ops
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Docker']
description: Docker学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/7caae012-71e8-11ef-a49e-ba1ea485754b.jpg
category: Docker
draft: false
---


# Introduction to Docker Compose | Baeldung on Ops

[Introduction to Docker Compose | Baeldung on Ops](https://www.baeldung.com/ops/docker-compose)

[Docker Compose 入门 | Baeldung 运维](https://www.baeldung.com/ops/docker-compose)

## **1. 概览**

当广泛使用Docker时，多个不同容器的管理很快就会变得繁琐。

Docker Compose是一个工具，帮助我们克服这个问题，可以**一次性轻松处理多个容器**。

在本教程中，我们将检查其主要功能和强大机制。

## **2. YAML配置说明**

简而言之，Docker Compose通过应用在**单个_docker-compose.yml_配置文件**中声明的许多规则来工作。

这些YAML规则，既适合人类阅读，也适合机器优化，提供了一种有效的方式来在几行内从高空快照整个项目。

几乎每条规则都替换了一个特定的Docker命令，以便最终，我们只需要运行：

```bash
docker-compose up
```

我们可以在底层获得Compose应用的数十种配置。这将节省我们使用Bash或其他脚本编写它们的麻烦。

在此文件中，我们需要指定Compose文件格式的*版本*，至少一个*服务*，以及可选的*卷*和*网络*：

```plaintext
version: "3.7"
services:
  ...
volumes:
  ...
networks:
  ...
```

让我们看看这些元素实际上是是什么。

### **2.1. 服务**

首先，**服务**指的是容器的配置。

例如，让我们以一个由前端、后端和数据库组成的容器化Web应用程序为例。我们可能会将这些组件分割成三个镜像，并在配置中将它们定义为三个不同的服务：

```plaintext
services:
  frontend:
    image: my-vue-app
    ...
  backend:
    image: my-springboot-app
    ...
  db:
    image: postgres
    ...
```

我们可以在服务上应用多种设置，我们将在稍后更详细地探索它们。

### **2.2. 卷和网络**

另一方面，**卷**是主机和容器之间共享的物理磁盘空间区域，甚至可以在容器之间共享。换句话说，**卷是主机中的一个共享目录**，可以从一些或所有容器中看到。

同样，**网络**定义了容器之间的通信规则，以及容器和主机之间的通信规则。公共网络区域将使容器的服务能够相互发现，而私有网络区域将它们隔离在虚拟沙箱中。

再次，我们将在下一节中了解更多信息。

## **3. 剖析服务**

现在让我们开始检查服务的主要设置。

### **3.1. 拉取镜像**

有时，我们的服务所需的镜像已经在[Docker Hub](https://hub.docker.com/)或另一个Docker注册表中发布（由我们或其他人发布）。

如果是这种情况，那么我们将通过指定镜像名称和标签的*image*属性来引用它：

```plaintext
services: 
  my-service:
    image: ubuntu:latest
    ...
```

### **3.2. 构建镜像**

或者，我们可能需要从源代码构建一个镜像，通过读取其*Dockerfile*。

这次，我们将使用*build*关键字，将Dockerfile的路径作为值传递：

```plaintext
services: 
  my-custom-app:
    build: /path/to/dockerfile/
    ...
```

我们也可以[使用URL](https://gist.github.com/derianpt/420617ffa5d2409f9d2a4a1a60cfa9ae#file-build-contexts-yml)而不是路径：

```plaintext
services: 
  my-custom-app:
    build: https://github.com/my-company/my-project.git 
    ...
```

此外，我们可以与*build*属性一起指定*image*名称，一旦创建，将命名镜像，[使其可供其他服务使用](https://stackoverflow.com/a/35662191/1654265)：

```plaintext
services: 
  my-custom-app:
    build: https://github.com/my-company/my-project.git 
    image: my-project-image
    ...
```

### **3.3. 配置网络**

**Docker容器在由Docker Compose创建的网络中相互通信**。同一网络上的一个服务可以通过简单地引用容器名称和端口（例如*network-example-service:80*）与另一个服务通信，前提是我们已经通过*expose*关键字使端口可访问：

```plaintext
services:
  network-example-service:
    image: karthequian/helloworld:latest
    expose:
      - "80"
```

在这种情况下，即使不暴露它也可以工作，因为*expose*指令已经在[镜像Dockerfile](https://github.com/karthequian/docker-helloworld/blob/master/Dockerfile#L45)中。

**要从主机访问容器**，**端口必须通过**​***ports***​**关键字声明性地暴露**，这也允许我们选择是否在主机上以不同的方式暴露端口：

```plaintext
services:
  network-example-service:
    image: karthequian/helloworld:latest
    ports:
      - "80:80"
    ...
  my-custom-app:
    image: myapp:latest
    ports:
      - "8080:3000"
    ...
  my-custom-app-replica:
    image: myapp:latest
    ports:
      - "8081:3000"
    ...
```

现在，端口80将从主机可见，而其他两个容器的端口3000将在主机的端口8080和8081上可用。**这种强大的机制允许我们运行不同的容器，暴露相同的端口而不发生冲突**。

最后，我们可以定义额外的虚拟网络来隔离我们的容器：

```plaintext
services:
  network-example-service:
    image: karthequian/helloworld:latest
    networks: 
      - my-shared-network
    ...
  another-service-in-the-same-network:
    image: alpine:latest
    networks: 
      - my-shared-network
    ...
  another-service-in-its-own-network:
    image: alpine:latest
    networks: 
      - my-private-network
    ...
networks:
  my-shared-network: {}
  my-private-network: {}
```

在最后一个示例中，我们可以看到*another-service-in-the-same-network*将能够ping并到达*network-example-service*的端口80，而*another-service-in-its-own-network*则不能。

### **3.4. 设置卷**

有三种类型的卷：*匿名*、*命名*和*主机*。

**Docker管理匿名和命名卷**，在主机中自动将它们挂载到自动生成的目录中。虽然匿名卷在Docker的旧版本（1.9之前）中很有用，但现在建议使用命名卷。**主机卷还允许我们指定主机中的现有文件夹**。

我们可以在服务级别配置主机卷，并在配置的外部级别配置命名卷，以便使后者对其他容器可见，而不仅仅是它们所属的一个：

```plaintext
services:
  volumes-example-service:
    image: alpine:latest
    volumes: 
      - my-named-global-volume:/my-volumes/named-global-volume
      - /tmp:/my-volumes/host-volume
      - /home:/my-volumes/readonly-host-volume:ro
    ...
  another-volumes-example-service:
    image: alpine:latest
    volumes:
      - my-named-global-volume:/another-path/the-same-named-global-volume
    ...
volumes:
  my-named-global-volume: 
```

在这里，两个容器将对*my-named-global-volume*共享文件夹拥有读写访问权限，无论它们将其映射到哪个路径。相反，两个主机卷将仅对*volumes-example-service*可用。

主机文件系统的\*/tmp*文件夹映射到容器的*/my-volumes/host-volume\*文件夹。这个文件系统部分是可写的，这意味着容器可以读取以及在主机机器上写入（和删除）文件。

**我们可以通过在规则中附加**\*:ro***来以只读模式挂载卷***​ *，就像*/home\*文件夹一样（我们不希望Docker容器意外删除我们的用户）。

### **3.5. 声明依赖关系**

通常，我们需要在服务之间创建依赖链，以便某些服务在其他服务之前（和之后）加载。我们可以通过*depends_on*关键字实现这个结果：

```plaintext
services:
  kafka:
    image: wurstmeister/kafka:2.11-0.11.0.3
    depends_on:
      - zookeeper
    ...
  zookeeper:
    image: wurstmeister/zookeeper
    ...
```

然而，我们应该意识到，Compose不会等待*zookeeper*服务完成加载后再启动*kafka*服务；它只会等待它启动。如果我们需要一个服务在启动另一个服务之前完全加载，我们需要在Compose中获得[更深入的启动和关闭顺序控制](https://docs.docker.com/compose/startup-order/)。

## **4. 管理环境变量**

在Compose中使用环境变量很容易。我们可以定义静态环境变量，以及使用\*\${}\*符号的动态变量：

```plaintext
services:
  database: 
    image: "postgres:${POSTGRES_VERSION}"
    environment:
      DB: mydb
      USER: "${USER}"
```

为Compose提供这些值有不同的方法。

例如，一种方法是在同一个目录中设置\*.env*文件，结构就像*.properties\*文件，*key=value*：

```plaintext
POSTGRES_VERSION=alpine
```

复制再试一次分享

​![](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/7db9f5cd-71e8-11ef-a5c5-ba1ea485754b.png)​

USER\=foo

```text

否则，我们可以在调用命令之前在操作系统中设置它们：

‍‍```plaintext
export POSTGRES_VERSION=alpine
export USER=foo
docker-compose up
```

最后，我们可能会发现在shell中使用一个简单的单行命令很容易：

```plaintext
POSTGRES_VERSION=alpine USER=foo docker-compose up
```

我们可以混合这些方法，但让我们记住Compose使用以下优先级顺序，用较高优先级覆盖较低优先级：

1. Compose文件
2. Shell环境变量
3. 环境文件
4. Dockerfile
5. 未定义的变量

## **5. 扩展和副本**

在旧版的Compose中，我们可以通过*docker-compose scale*命令来扩展容器实例。新版本弃用了它，并用\*–scale\*选项替换。

我们可以利用[Docker Swarm](https://docs.docker.com/engine/swarm/)，一个Docker引擎集群，并在*deploy*部分的*replicas*属性中声明性地自动扩展我们的容器：

```plaintext
services:
  worker:
    image: dockersamples/examplevotingapp_worker
    networks:
      - frontend
      - backend
    deploy:
      mode: replicated
      replicas: 6
      resources:
        limits:
          cpus: '0.50'
          memory: 50M
        reservations:
          cpus: '0.25'
          memory: 20M
      ...
```

在*deploy*下，我们还可以指定许多其他选项，如资源阈值。然而，Compose**只有在部署到Swarm时才考虑整个**​***deploy***​**部分**，否则会忽略它。

## **6. 真实世界的例子：Spring Cloud Data Flow**

虽然小型实验有助于我们理解单个齿轮，但看到真实世界的代码在行动中肯定会揭示全貌。

Spring Cloud Data Flow是一个复杂的项目，但足够简单，易于理解。让我们[下载它的YAML文件](https://dataflow.spring.io/docs/installation/local/docker/)并运行：

```plaintext
DATAFLOW_VERSION=2.1.0.RELEASE SKIPPER_VERSION=2.0.2.RELEASE docker-compose up 
```

Compose将下载、配置并启动每个组件，然后将**容器的日志交叉到当前终端的单个流中**。

它还将为它们每一个应用独特的颜色，以获得极佳的用户体验：

[https://www.baeldung.com/wp-content/uploads/sites/6/2023/03/Screenshot-from-2019-05-22-01-37-52-300x169.png](https://www.baeldung.com/wp-content/uploads/sites/6/2023/03/Screenshot-from-2019-05-22-01-37-52-300x169.png)

我们可能会在运行全新的Docker Compose安装时遇到以下错误：

```plaintext
lookup registry-1.docker.io: no such host
```

虽然[有不同解决方案](https://stackoverflow.com/questions/46036152/lookup-registry-1-docker-io-no-such-host)来解决这个常见陷阱，但使用*8.8.8.8*作为DNS可能是最简单的。

## **7. 生命周期管理**

现在让我们仔细看看Docker Compose的语法：

```plaintext
docker-compose [-f <arg>...] [options] [COMMAND] [ARGS...]
```

虽然有[许多选项和命令可用](https://docs.docker.com/compose/reference/overview/)，我们至少需要知道正确激活和停用整个系统的方法。

### **7.1. 启动**

我们已经看到，我们可以使用*up*创建并启动配置中定义的容器、网络和卷：

```plaintext
docker-compose up
```

然而，第一次之后，我们可以使用*start*来启动服务：

```plaintext
docker-compose start
```

如果我们的文件名与默认文件名（*docker-compose.yml*）不同，我们可以利用\*-f*和*–file\*标志来指定一个替代的文件名：

```plaintext
docker-compose -f custom-compose-file.yml start
```

Compose也可以在启动时使用\*-d\*选项作为守护进程在后台运行：

```plaintext
docker-compose up -d
```

### **7.2. 关闭**

要安全地停止活动服务，我们可以使用*stop*，它将保留容器、卷和网络，以及对它们的所有修改：

```plaintext
docker-compose stop
```

要重置我们项目的状态，我们只需运行*down*，**它将销毁一切，除了外部卷**：

```plaintext
docker-compose down
```

## **8. 结论**

在本文中，我们了解了Docker Compose及其工作原理。

像往常一样，我们可以在[GitHub](https://github.com/Baeldung/ops-tutorials/tree/main/docker-modules/docker-compose)上找到源*docker-compose.yml*文件，以及以下图像中立即可用的有用测试套件：

[https://www.baeldung.com/wp-content/uploads/sites/6/2023/03/Tests1-300x233.webp](https://www.baeldung.com/wp-content/uploads/sites/6/2023/03/Tests1-300x233.webp)

---
本文是个人学习记录，如果有侵权请联系后删除。
