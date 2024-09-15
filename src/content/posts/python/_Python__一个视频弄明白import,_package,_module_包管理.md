---
title: ' Python  一个视频弄明白import, package, module 包管理'
published: 2024-09-13
tags: ['学习记录', '学习笔记', 'Python']
description: Python学习记录
image: https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/bda2262b28eed7229934658243c22de4906c802f464c17febdd7fb2f07d085a7.jpg
category: Python
draft: false
---


# [Python] 一个视频弄明白import, package, module 包管理

[[Python] 一个视频弄明白import, package, module 包管理_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1YweNe2EGa/?spm_id_from=333.788&vd_source=f5ab73e8b88cb4cb94d904126cdfeb27)

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/e4681217c2b263819d4b7b2de8c7440e0f0aaadeebae016695239bee167de2b3.png)通过import导入同级目录下的包。实际上是初始化了已给module然后赋值给一个变量，当然该变量同样可以传递。一种官方提供的方式![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/53b147b9ff300aea3aacb41b4b731ad3c56235024c0cb8290814142c75365200.png)​

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/f9ae3f4b865f4ceb6b1b0e62f5c05bcd62d1c0dac5f8e92b77ec8c5f05509828.png)说明module导入只会导入一次，第二次会赋值第一次的导入。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/a306cbb3d22eb6feb6544c4e410a20a514a482c5bdff73761d141be78576bce4.png)打印输出module下面的成员

其中mm就是module的全局命名空间。![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/98433e6593e816c08dcb5e8faba780e492d2e29dfc2467b7e53163e8c46407d8.png)其中的add_global函数是给mm的全局命名空间中增加一个变量。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/76a8a455553f9ec32398442b2c824248e29460dd453d79427d8712408b11f579.png)​

‍

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/27ff197dbecb6ebdb0aecfde7e5121c8cca1713369c6fe60d3f7aefeb0cce896.png)此时还是会初始化module并将module中PI变量赋值给当前命名空间中的PI变量。如果此时更改当前的命名空间的中的PI，则不会影响之前的module中的PI。

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/17135e26ad6fcdad499bdef39e9743f7645c8d51594e3244188bb62e2211f432.png)​

‍

import 从哪里去找对应的module？

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/31a12161d74fd504049e50ca1ebee26bf4dc3d376e5a3e1d769f50dc022e088b.png)从sys.path中去找。

可以通过环境变量的方式更改python的sys.path的路径![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/5fce394c6fd64dc59dcf8d5bc50061ca3ffeffa9e6bce4fd57690bd32fbb68da.png)​

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/9d5d21929059a8f8ad18cb5db20538d688f9908d876c5b81c29626547a182af3.png)当目录不存在时候，会使用mymath.py作为module，如果mymath目录存在，则优先寻找目录，并加载运行init module代码，如果init不存在，那么也会加载对应的module，不会运行任何的带啊吗

‍

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/7d8bd37b48dd4ba990ac445bff2648d6d2a2acc2e0402a517a60102f74ff691a.png)对于子目录，这样的导入，会再当前的空间中创建对应的mydir变量，并在mydir下创建subdir变量

‍

如果使用from mydir import subdir 这样的语句，会导入当前的命名空间中subdir，同样也会再mydir的命名空间中导入subdir

​![image](https://cdn.jsdelivr.net/gh/Flandre923/CDN/img/c17bfb3f66e00728e28fdc0aa961b1d4a9e61db6ae6459a6bb458f26e9ccc879.png)对于a想导入上级的module和想导入下级的module的方法。如果上级的上级则使用。。。表示。

‍

---
本文是个人学习记录，如果有侵权请联系后删除。
