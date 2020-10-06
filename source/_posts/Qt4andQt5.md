---
title: Qt4andQt5
toc: true
author: w-qhai
date: 2020-10-06 10:11:26
tags:
- Qt4
- Qt5
- Qt creator
categories:
- 开发环境
- windows
- Qt开发
---

# Qt creator Qt4 与 Qt5 环境搭建

教室里的嵌入式机器装的是Qt4，用习惯了新版的Qt creator再用旧版的，有点难以适应。

所以我就想：反正Qt creator只是个写代码的壳子，套在Qt5上可以，在Qt4上肯定也行

<!--more-->

## 提前准备

- Qt5 这个可以去国内镜像站下载，官方下载比较慢，已经安装的可以跳过这一步

![image-Qt5download](https://i.loli.net/2020/10/06/KhqPmylL3xRkbgF.png)

Qt5 自带新版Qt creator，比旧版的creator好用很多

`http://mirrors.ustc.edu.cn/qtproject/archive/qt/5.14/5.14.2/` 下载带windows字样的文件就可以了

下载完直接安装



- 下载MinGW

  我准备下4.8.7版本的Qt4

  **不同版本的Qt需要不同版本的MinGW，不要下错了！！！**

![image-mingwdownload](https://i.loli.net/2020/10/06/1Y2nfsjRaTvzA5B.png)

`https://wiki.qt.io/MinGW`

**下载好解压，等会要用**



- Qt4 sdk

  这个东西在国内镜像找不到了，只能去官网下载

  `http://download.qt.io/archive/qt/4.8/4.8.7/`
  
  ![image-Qt4download](https://i.loli.net/2020/10/06/IouHrDif7ORtYQN.png)

  下载也是安装就行，中间会让你选择MinGW的路径，找到刚才解压的文件，进入找到bin所在的路径，粘贴上就行

  **路径不要带着 `bin`**  点到为止

![image-mingwpath](https://i.loli.net/2020/10/06/D1kabGXMe6OZNd7.png)



## 环境搭建

- 打开Qt creator, 现在是Qt5的环境

  `工具->选项->Kits` 我们就是修改这里的内容

- 点开`编译器选项卡`

  `添加->MinGW` C/C++都要修改

  这以C++为例

    ![image-compilers](https://i.loli.net/2020/10/06/dwNXro4H8FLxpjI.png)

  **C     ==> gcc.exe**

  **C++ ==> g++.exe**

  

- 同样的方式 改一下Debuggers

  查找 **mingw/bin/gdb.exe**

- 接下来打开Qt Versions

  `添加` 然后找到你安装Qt4的目录，选择 **bin/qmake.exe**  前面没有红色感叹号 说明成功了
  
  ![image-Qt Versions](https://i.loli.net/2020/10/06/SbisAkG5BzZqQKl.png)

- 最后 构建套件(Kit)

  依旧点击添加，修改红色框起来的部分就可以了

  ![image-Kits](https://i.loli.net/2020/10/06/Expvm51sQe3RLkD.png)

环境搭建完成！

## 测试

新建项目，可以选一个 也可以两个都选

![image-newporject](https://i.loli.net/2020/10/06/zMcno6lhbrdCLeg.png)

新建的项目 会有这些警告，可以编译可以运行，就是警告看着难受。

![image-warnings3](https://i.loli.net/2020/10/06/IFYs6K5N4AzpJPu.png)

`帮助->关于`把这个插件关掉就行了。

![image-plugins](https://i.loli.net/2020/10/06/UQSkdtlT3V5IEKg.png)



**Qt4 不支持`nullptr`关键字，要手动改成0或者NULL**

```cpp
#include <QWidget>

QT_BEGIN_NAMESPACE
namespace Ui { class Widget; }
QT_END_NAMESPACE

class Widget : public QWidget
{
    Q_OBJECT

public:
//    Widget(QWidget *parent = nullptr);
    Widget(QWidget *parent = 0);
    ~Widget();

private:
    Ui::Widget *ui;
};
```




## 参考资料
> - []()
> - []()
