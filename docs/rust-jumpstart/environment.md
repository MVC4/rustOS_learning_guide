---
description: “今天配了一天的环境” —— 某（些）无奈的学长
---
# 环境配置

在任何平台上进行任何的编程之前，我们都需要进行环境的配置，以确保计算机有正确的工具和库可以让程序可以编译和运行，否则看到自己明明写了正确的程序，却无论如何无法正确地编译和运行是非常令人沮丧的。

“环境”一词包含着很多层内容，基本上涵盖了计算机程序运行的方方面面：从硬件条件、操作系统、编译工具链到用户库文件，都在“环境”的范畴内。我们在 Introduction 章节已经引导使用 Windows 操作系统的同学安装了 Ubuntu 18.04 作为实验用的操作系统，这也是环境配置的其中一个环节。我们现在拥有了统一的操作i同，现在比较关注的是安装 Rust 工具链，来让我们使用 Rust 代码编写的文件可以运行起来。

## RTM (Read The Manual)

对于任何一门程序设计语言来说，让人们能够快速地配置好环境并且成功运行第一个程序是它的重中之重。一般来说，语言的官方文档的第一节就会提到这件事情。所以我们现在不会再花太多的时间详细引导你进行环境的配置，你可以参考下面的官方文档，又或者是你可以在网络上寻找更加简单的说明对 Rust 的工具链进行安装。我们这里负责给出一些解答与提示。

- [官方英文文档](https://doc.rust-lang.org/book/ch01-01-installation.html)
- [官方简体中文文档](https://kaisery.github.io/trpl-zh-cn/ch01-01-installation.html)

### 安装缺失的软件

如果系统有类似如下的提示：

```sh
Command 'xxx' not found, but can be installed with:

sudo apt install xxx
```

说明有的指令所对应的软件还没有被安装，你需要使用`sudo apt install`指令进行安装。

根据测试，如果你直接使用的是 WSL 的话，那么基本上所有有关编程的工具都已经给你安装好了。可以很顺利地直接安装 Rust

但是 Ubuntu18.04.5的镜像中缺少一些东西，比如说 curl和链接器，这使得直接使用这个镜像会有一点困难。你需要首先使用`sudo apt install`指令安装如下的两个内容：

```sh
sudo apt install curl
sudo apt install gcc
```

#### 换源

如果你处于中国大陆，那么可能这些软件的下载速度会非常慢。这时我们可以修改一下下载的地址来源，切换为国内的镜像，不过过程比较复杂。你可以参考[这篇简书文章](https://www.jianshu.com/p/20f2186d9cbb)进行配置

### rustup 安装

安装好 rustup 后只需要根据默认选项按回车就可以了。

在完全安装完毕后可以选择重启来配置环境变量，或者可以运行命令行中提示的`source $HOME/.cargo/env`使得当前命令行可以使用对应的变量，但是在你重启之前，你的其他命令行都需要重新配置环境变量。

p.s. 如果你不知道什么是环境变量而且想要省一点事，就在安装过后直接重启就可以了。

现在你已经跟随着官方文档完成了 rustup 的安装以及 Rust 编译环境的配置。你应该运行过下面的指令，并且确定它有正确的输出了：

```sh
rustc --version

> rustc 1.47.0 (18bf6b4f0 2020-10-07) # 类似这样的输出
```

完成到这里基本上我们就可以说我们针对 Rust 的编程环境已经搭建好了。做了这么多工作，我们现在终于可以进入 Rust 的世界了，真正的 Rust Jumpstart 就要开始了。

## 环境配置碎碎念

配环境绝对就是每一个程序员的噩梦，无论是高层的开发还是底层的开发，环境始终是让人的头疼的事情。因为有的时候配置的工具差了一点点都可能使得整个程序无法运行，有的时候怎么检查都检查不出来错误，结果最后是环境配置中出了一些问题，真的让人非常火大。

在底层开发中最为头疼的事情莫过于交叉编译了，这是指我们在一个平台上生成一个在另一个平台上运行的程序，因为计算机的底层架构不一样，所以编译出来的程序不一定在不同的电脑上都能跑起来，这时候就需要进行交叉编译。如果交叉编译的工具链没有配置好，发现自己写的程序编译不了，上网找解决方法的话非常困难，因为这些交叉编译工具报的错可能并不能提供什么帮助，需要自己找到问题。

在高层开发最为基础的环境问题就是操作系统，不同的操作系统能给你提供的工具都是不一样的。还有一个需要处理的问题就是包管理，也就是我们需要使用其他人写的代码作为“轮子”进行复用。如果没有很好的包管理工具，那么多个人在协作的时候，或是在不同的平台上配置项目的时候，为了把各个依赖的包安装好就能让人头疼一阵。

### 环境碎碎念

“环境”这个词汇可能没有非常确切的定义。很基础的一个理解就是：为了完成我的目标，我所需要的东西。一般来说，程序员都是希望程序能够在计算机上运行（可能还有别的需求，比如说测试什么的），那么为了让程序在一个特定的计算机上运行，有很多的条件需要满足，这些条件应该可以统称是环境。（但是*电脑需要插电*算不算环境呢？至少目前看来应该不算）

计算机的环境实际上非常复杂，最为底层的 CPU 的架构就是不一样的。我们经常听说的 Intel 和 ARM 两家公司生产的 CPU 的架构就是不一样的，这导致如果你有一个二进制的可执行文件，你一般是不能让这个文件同时支持在两个 CPU 的架构上运行的。计算机产业的人们花了很长的时间研究了各种方法让一个程序能够不需要修改和额外的说明的情况下在不同的 CPU 上运行，因此也产生了非常多有趣的产物。

硬件上还有一些别的环境依赖，比如说各类外设，能不能联网，能不能输出图像等等。

在 CPU 架构以及指令集之上就是操作系统。操作系统的影响就不必多说了，许多 Windows 用户很希望使用 Mac 上的软件，但是无奈没有对应的 Windows 版本就可以理解操作系统的影响了。

操作系统再往上就是各类用户库以及用户程序，有的时候这些东西也很让人头疼。如果你写过 Qt 的代码的话你就能产生这种感觉，因为要生成一个可以独立运行的 Qt 代码你需要一些配置一些动态链接库，如果目标平台并没有安装 Qt 的话你就需要打包附上所有需要的动态链接库。在这期间产生的一些程序依赖也非常难发现。