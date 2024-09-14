---
title: 安装Docker
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Docker']
description: Docker学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/7e68f8e3-71e8-11ef-b29b-ba1ea485754b.jpg
category: Docker
draft: false
---


# 安装Docker

# 安装docker for desktop 同时会安装 docker compose

[Install Docker Desktop on Ubuntu | Docker Docs](https://docs.docker.com/desktop/install/ubuntu/) 参考这个流程

# 安装docker 第一步

1. 先去安装docker [Install Docker Engine on Ubuntu | Docker Docs](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

```gdscript
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

```

```console
 sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

```console
 sudo docker run hello-world
```

启动一个hello world 查看是否启动成功了。

1. 下载[deb package](https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64&_gl=1*vny7yg*_gcl_au*NzYzMDQ4NDQ3LjE3MjQ5MzAyODI.*_ga*MTM3MjA2NjIwLjE3MTY3MzM4NDE.*_ga_XJWPQMJYHQ*MTcyNDkyOTk5OS4zLjEuMTcyNDkzMjI3OC41MS4wLjA)

3. ```gdscript

    # 通过这个代码安装
     sudo apt-get update
     sudo apt-get install ./docker-desktop-<arch>.deb
    ```

默认情况下，Docker Desktop 安装在 `/opt/docker-desktop`​ 。 

​![image-20240829200026-fhsbzzn](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/7fba4c38-71e8-11ef-aa86-ba1ea485754b.png)​

添加策略组，让当前的用户可以访问

‍

‍

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
