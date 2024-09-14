---
title: 使用VScode创建工程并添加测试
published: 2024-09-13
tags: ['C#', 'Tutorial']
description: C#学习记录
image: 
category: C#
draft: false
---


# 使用VScode创建工程并添加测试

​`dotnet new sln`​ 创建一个sln

​`dotnet new console -o Averages `​

​`dotnet new mstest -o Averages.Tests`​

​`dotnet sln add ./Averages/Averages.csproj`​

​`dotnet sln add ./Averages.Tests/Averages.Tests.csproj`​

​`dotnet add ./Averages.Tests/Averages.Tests.csproj reference ./Averages/Averages.csproj`​ 将第二个项目作为第一个项目的引用

---
本文是个人学习记录，如果有侵权请联系后删除。
