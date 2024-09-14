---
title: [Python] 一个视频弄明白import, package, module 包管理
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/e6628da3-71e8-11ef-a7a0-ba1ea485754b.png
category: Python
draft: false
---


# [Python] 一个视频弄明白import, package, module 包管理

[[Python] 一个视频弄明白import, package, module 包管理_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1YweNe2EGa/?spm_id_from=333.788&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f69b556b-71e8-11ef-9c78-ba1ea485754b.png)通过import导入同级目录下的包。实际上是初始化了已给module然后赋值给一个变量，当然该变量同样可以传递。一种官方提供的方式![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f7821b86-71e8-11ef-b180-ba1ea485754b.png)​

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f819f149-71e8-11ef-a36f-ba1ea485754b.png)说明module导入只会导入一次，第二次会赋值第一次的导入。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f8fff396-71e8-11ef-843f-ba1ea485754b.png)打印输出module下面的成员

其中mm就是module的全局命名空间。![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f9ecc494-71e8-11ef-aaff-ba1ea485754b.png)其中的add_global函数是给mm的全局命名空间中增加一个变量。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/faf0ea25-71e8-11ef-bb32-ba1ea485754b.png)​

‍

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/fde15bc9-71e8-11ef-93a3-ba1ea485754b.png)此时还是会初始化module并将module中PI变量赋值给当前命名空间中的PI变量。如果此时更改当前的命名空间的中的PI，则不会影响之前的module中的PI。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/00687917-71e9-11ef-887a-ba1ea485754b.png)​

‍

import 从哪里去找对应的module？

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/014ea292-71e9-11ef-931a-ba1ea485754b.png)从sys.path中去找。

可以通过环境变量的方式更改python的sys.path的路径![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/027bc7c6-71e9-11ef-bbf6-ba1ea485754b.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/0375ad55-71e9-11ef-b5cd-ba1ea485754b.png)当目录不存在时候，会使用mymath.py作为module，如果mymath目录存在，则优先寻找目录，并加载运行init module代码，如果init不存在，那么也会加载对应的module，不会运行任何的带啊吗

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/048bcc94-71e9-11ef-ba05-ba1ea485754b.png)对于子目录，这样的导入，会再当前的空间中创建对应的mydir变量，并在mydir下创建subdir变量

‍

如果使用from mydir import subdir 这样的语句，会导入当前的命名空间中subdir，同样也会再mydir的命名空间中导入subdir

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/05beae66-71e9-11ef-abf5-ba1ea485754b.png)对于a想导入上级的module和想导入下级的module的方法。如果上级的上级则使用。。。表示。

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
