---
title: windows下python jupyter tensorflow-gpu环境搭建
toc: true
author: w-qhai
date: 2019-07-22 21:30:48
tags:
- python
- 机器学习
categories:
- 开发环境
- windows
- python开发
---

## python基本环境搭建

- 首先`https://www.python.org/downloads/windows/`下载对应版本的python

- 安装的时候注意一下几点就ok， 选择自定安装是为了更改安装目录， 如果想安装早C盘， 直接点第一个就行，然后无脑next
<!--more-->

  ![install](https://iqxqzx.gitee.io/pic/images/2019/7/22/python_install_01.png)

- 检查一下是否安装好了

  ![cmd](https://iqxqzx.gitee.io/pic/images/2019/7/22/python_cmd_02.png)

  出现'>>>'就表示安装好了

- 打开cmd 输入`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ jupyter`

  -i 是表示用国内源， 清华的比较快

- 然后打开cmd输入`jypyter notebook` 大功告成





## tensorflow环境搭建（需要vs2015或者以上版本）

- 试一下在jupyter里`import tensorflow`

  ![tensorflow](https://iqxqzx.gitee.io/pic/images/2019/7/22/python_tensorflow_03.png)

  不出意外会有这个报错，所以我们就要去下载cuda 10.0， 后面的链接是给的9.0， 不用管，让下什么版本就下什么版本，不要没事找事。

- `https://developer.nvidia.com/cuda-10.0-download-archive` cuda 10.0的下载地址

  ![cuda](https://iqxqzx.gitee.io/pic/images/2019/7/22/python_cuda_04.png)

  本地版应该比网络版快，点击下载就ok，下载完安装，全部默认，不知道啥用就不要改了。

- 还需要下载cudnn，这个要注册之后才能下载

  ![cudnn](https://iqxqzx.gitee.io/pic/images/2019/7/22/cudnn.png)

  下载与cuda对应版本即可， 之后解压， 把解压之后的东西， 放到`C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0`对应目录下

- 接下来配置环境变量：

  计算机上点右键，打开属性->高级系统设置->环境变量，可以看到系统中多了CUDA_PATH和CUDA_PATH_V8_0两个环境变量，接下来，还要在系统中添加以下几个环境变量：

  `CUDA_SDK_PATH = C:\ProgramData\NVIDIA Corporation\CUDA Samples\v10.0
  CUDA_LIB_PATH = %CUDA_PATH%\lib\x64
  CUDA_BIN_PATH = %CUDA_PATH%\bin
  CUDA_SDK_BIN_PATH = %CUDA_SDK_PATH%\bin\win64
  CUDA_SDK_LIB_PATH = %CUDA_SDK_PATH%\common\lib\x64`'

- 在系统变量 PATH 的末尾添加：
  `CUDA_LIB_PATH%;%CUDA_BIN_PATH%;%CUDA_SDK_LIB_PATH%;%CUDA_SDK_BIN_PATH%;`
  再添加如下4条（默认安装路径）：
  `:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\lib\x64；
  C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\bin；
  C:\ProgramData\NVIDIA Corporation\CUDA Samples\v8.0\common\lib\x64；
  C:\ProgramData\NVIDIA Corporation\CUDA Samples\v8.0\bin\win64；`

- 打开`cd C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\extras\demo_suite`

  然后分别执行`bandwidthTest.exe`和`deviceQuery.exe`。

  如果都返回Result=PASS就是配置成功了。

- 进入python`import tensorflow`啥都没发生，好了可以写代码了。



## 参考资料
- []()
- []()
