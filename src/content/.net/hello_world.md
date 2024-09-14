---
title: hello world
published: 2024-09-13
tags: ['C#', 'Tutorial']
description: C#学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/ca912dc5-71ea-11ef-a6c2-ba1ea485754b.jpg
category: C#
draft: false
---


# hello world

# hello world

我们之前安装了dotnet，下面来看一个程序吧。

我们创建第一个程序

```bash
 $ dotnet new console -o 01-hello-world
The template "Console App" was created successfully.

Processing post-creation actions...
Restoring /workspaces/ubuntu/01-hello-world/01-hello-world.csproj:
  Determining projects to restore...
  Restored /workspaces/ubuntu/01-hello-world/01-hello-world.csproj (in 1.5 sec).
Restore succeeded.
```

cd到对应的目录下

```bash
cd 01-hello-world
```

创建了一个控制台项目

```bash
// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");
```

打印输出一个hello world

通过dotnet build生成可执行文件，在同级目录下的bin文件夹中

```bash
$ dotnet build 
MSBuild version 17.8.5+b5265ef37 for .NET
  Determining projects to restore...
  All projects are up-to-date for restore.
  01-hello-world -> /workspaces/ubuntu/01-hello-world/bin/Debug/net8.0/01-hello-world.dll

Build succeeded.
    0 Warning(s)
    0 Error(s)

```

```bash
./bin/Debug/net8.0/01-hello-world 
Hello, World!
```

通过dotnet run运行可执行文件

```bash
$ dotnet run 
Hello, World!
```

vscode 安装c#拓展

c# dev kit

安装了这个就有代码补全了。

‍

# 注解

```bash
// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");

```

// 开头的就是注解，注解不会运行，目的是为了给你的代码讲解功

```bash
/* 
 多行注解
*/
```

标准输出到命令行中

```bash
Console.WriteLine("Hello, World!");
```

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
