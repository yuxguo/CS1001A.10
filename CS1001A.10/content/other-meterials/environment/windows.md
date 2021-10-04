---
title: "在Windows上搭建C/C++环境"
---

在我们开始之前，先要弄清楚我们在搭建一个用于做什么的 C/C++ 环境。一个 C/C++ 环境最基础的要求是舒适的代码编写体验（包括智能提示、代码高亮等）以及便利的编译调试功能（包括源码编译、链接、生成可执行文件等）。我们既可以分别配置**代码编辑器**和编译器来完成环境的搭建，也可以直接选用**集成开发环境（IDE，Integrated Development Environment）** 来进行程序开发。

因此我们提供了如下两种不同的环境搭建方式，大家自行选择：

- [**VSCode** + **MinGW-w64**](#轻量化工作拥抱全宇宙最好用的编辑器-vscode)
- [**Visual Studio Community**](#重量级嘉宾走向全宇宙最好用的ide-visual-studio)

## 轻量化工作——拥抱全宇宙最好用的编辑器 VSCode

VSCode 全称 Visual Studio Code，是微软开发的轻量级代码编辑器。MinGW 全称 Minimalist GNU on Windows，是开源编译器 GCC 在 Windows 下的移植版，现在被与之相比可以编译生成64位或32位可执行程序的 MinGW-w64 取代。

### 下载安装

#### VSCode

在[官网](https://code.visualstudio.com/Download)下载 Windows 稳定版，默认下一步即可

#### MinGW-w64

##### 下载解压

MinGW-w64 的代码文件被托管于[SourceForge](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/)上，注意**不要点击**最显眼的绿色 Download Latest Version 按钮，在页面下方 MinGW-W64 GCC-8.1.0 标题下的链接 x86_64-posix-seh ，或者点击[这里](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-posix/seh/x86_64-8.1.0-release-posix-seh-rt_v6-rev0.7z)直接下载。将下载得到的 .7z 压缩文件，并将其中的 mingw64 文件夹放置在合适的位置。例如`D:\mingw64`

##### 环境变量

为了让 Windows 系统识别编译器路径，我们需要手动将 MinGW-w64 的编译器路径添加到环境变量中：

1. `Win + S`搜索“系统环境变量”
3. 高级：环境变量
3. 编辑系统变量中的`Path`
4. 新建：`D:\mingw64\bin`

##### 测试

接下来打开命令提示符或 Powershell 终端，输入`gcc -v`，如果前述步骤正确，会有一段以 GCC 当前版本结尾的信息输出，证明我们的安装成功。

![0-version](/~gyx_20170818/CS1001A.10/Windows/VSCode/0-version.png)

### 在VSCode中调试运行C/C++文件

#### 安装拓展

在工作目录下右键，点击“通过 Code 打开”，点击最左侧的“拓展”选项卡，搜索安装如下拓展：

- Chinese (Simplified) Language Pack for Visual Studio Code
![2-Chinese](/~gyx_20170818/CS1001A.10/Windows/VSCode/2-Chinese.png)
- C/C++
![3-C++](/~gyx_20170818/CS1001A.10/Windows/VSCode/3-C++.png)

#### 测试运行

新建一个C++文件`HelloWorld.cpp`，在其中输入一些代码

```C++
#include<iostream>

using namespace std;
int main()
{
    cout << "HelloWorld" << endl;
    return 0;
}
```

点击`F5`并依次选择：

- 环境：C++(GDB/LLDB)
![4-run](/~gyx_20170818/CS1001A.10/Windows/VSCode/4-run.png)
- 配置：g++.exe - 生成和调试活动文件 编译器：D:\mingw64\bin\g++.exe
![5-run](/~gyx_20170818/CS1001A.10/Windows/VSCode/5-run.png)

首次调试运行，VSCode 会自动生成相应的配置文件`.vscode\task.json`与`.vscode\launch.json`，并编译运行程序，运行结果将出现在终端选项卡中。
![6-finish](/~gyx_20170818/CS1001A.10/Windows/VSCode/6-finish.png)

此后的程序运行只需要点击`F5`即可。

### VSCode工作环境简介

#### 工作区

VSCode工作环境的基本概念是“**工作区**”，如果一个文件夹下有`.vscode`文件夹，这个父文件夹就被VSCode认为是一个工作区。`.vscode`文件夹下包括了用以配置工作区环境的`.json`文件，其中`settings.json`存放了了工作区设置，这些设置会被用户设置所覆盖，详见VSCode的设置界面。除了每个工作区可以保存不同的设置外，也可以在不同的工作区中开启或禁用不同的插件来提升响应速度。

#### 后续配置

在网上多数VSCode+C/C++的教程文章中都有较大篇幅的设置文件，主要是通过修改工作区文件夹中`.vscode`文件夹中的`*.json`进行配置，这里不做赘述，可以自行参考修改。



## 重量级嘉宾——走向全宇宙最好用的IDE Visual Studio

Visual Studio 简称 VS，是微软公司的开发工具包系列产品。VS 是一个基本完整的开发工具集，它包括了整个软件生命周期中所需要的大部分工具。

### 下载安装

- 在[官网](https://visualstudio.microsoft.com/zh-hans/downloads/)下载 Visual Studio 2019 社区版安装器的安装器

- 打开安装器 Visual Studio Installer

- 选择 Visual Studio 2019 Community 社区版

- 在工作负荷中勾选“使用 C++ 的桌面开发”
![0-install](/~gyx_20170818/CS1001A.10/Windows/VS/0-install.png)

- 在语言包中勾选“中文(简体)”
![1-language](/~gyx_20170818/CS1001A.10/Windows/VS/1-language.png)

- 在安装位置中确认安装路径，且不要包括中文（请养成软件路径中不包括中文的好习惯）
![2-path](/~gyx_20170818/CS1001A.10/Windows/VS/2-path.png)

- 开始安装

### 测试运行

- 打开 Visual Studio 2019 Community 社区版
![3-opening](/~gyx_20170818/CS1001A.10/Windows/VS/3-opening.png)

- 在启动器中点击“创建新项目”
![4-launcher](/~gyx_20170818/CS1001A.10/Windows/VS/4-launcher.png)

- 依次选择“语言：C++”、“平台：Windows”，点选“控制台应用”
![5-new-project](/~gyx_20170818/CS1001A.10/Windows/VS/5-new-project.png)
> 注意：如果需要创建C语言项目，并尽可能减少C++相关依赖，那么点选“空项目”，并在之后手动修改源文件后缀名为`.c`

- 在配置新项目的界面中输入项目名称与位置，并勾选“将解决方案和项目放在同一目录中”
![6-creating](/~gyx_20170818/CS1001A.10/Windows/VS/6-creating.png)

- 在主界面中依次点击“调试”->“开始调试
![8-debug](/~gyx_20170818/CS1001A.10/Windows/VS/8-debug.png)

- 在弹出的终端中查看输出
![9-debug-result](/~gyx_20170818/CS1001A.10/Windows/VS/9-debug-result.png)
> 注意：默认情况下调试结束后控制台终端会自动关闭，导致结果一闪而过。如果发生这种现象，那么取消“工具”->“选项”->“调试”->“调试停止时自动关闭控制台”。或者点击“调试”->“开始执行(不调试)”
![run](/~gyx_20170818/CS1001A.10/Windows/VS/run.png)
![result](/~gyx_20170818/CS1001A.10/Windows/VS/result.png)

### Visual Studio 工作环境简介

Visual Studio 工作环境主要由“**项目**”和“**解决方案**”两个概念组成。

#### 项目

从逻辑上讲，项目包含所有编译为可执行文件、库或网站的文件。 这些文件可以包括源代码、图标、图像、数据文件等。 项目还包含编译器设置以及程序将与之通信的各种服务或组件需要的其他配置文件。

#### 解决方案

项目包含在解决方案中。 尽管其名称如此，但解决方案并不是“答案”。 解决方案只是一个容器，用于包含一个或多个相关项目，以及生成信息、Visual Studio 窗口设置和不与特定项目关联的任何杂项文件。

#### “项目和解决方案并不是必须的”

参见[在 Visual Studio 中开发代码而无需创建项目或解决方案](https://docs.microsoft.com/zh-cn/visualstudio/ide/develop-code-in-visual-studio-without-projects-or-solutions?view=vs-2019)

#### 深入理解

如果对Visual Studio的C++开发环境有兴趣，可以参见[官方的文档](https://docs.microsoft.com/zh-cn/visualstudio/ide/?view=vs-2019)，从一个[控制台计算器](https://docs.microsoft.com/zh-cn/cpp/get-started/tutorial-console-cpp?view=msvc-160)继续探索。