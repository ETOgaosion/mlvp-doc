---
title: MLVP文档 - 安装与配置
summary: MLVP Preparation
authors:
    - BlueSpace
date: 2023-11-01
---

# MLVP安装与配置

## Prerequests

- System:
    - Ubuntu 20.04
    - MacOS host, remote/VM(System Ubuntu 20.04):
        - orbstack [recommanded]
        - Linux remote server
        - docker
        - VMWare
        - VirtualBox
    - Windwos host, remote/VM(System Ubuntu 20.04):
        - WSL2 [recommanded]
        - WSL
        - Linux remote server
        - VMWare
        - VirtualBox
- Shell: zsh [recommanded]
- IDE:
    - 若使用VSCode，推荐使用clangd插件，获得和JetBrains CLion同等效果的代码检查和参数查看功能，
    - 若使用VS，推荐Resharper插件
    - Rider
    - CLion

## Dependencies Installation

### 软件源

```sh
sudo apt update
sudo apt install -y binutils gcc-10 g++-10 python3 python3-pip git help2man \
                    perl python3 make libfl2 libfl-dev zlibc zlib1g zlib1g-dev \
                    ccache mold libgoogle-perftools-dev numactl \
                    perl-doc autoconf flex bison clang clang-format \
                    cmake gdb graphviz lconv gtkwave unzip zip
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-10 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-10 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 10
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 10
```

若您使用VSCode配合CMake插件，我们建议您使用Clang 10+或者g++-10作为编译器，具体操作方法：在项目中根目录按`command`(mac)/`ctrl`(windows) + `shift` + `P`，输入`CMake: Select a kit`，而后选择您希望是哟的编译器，**注意本项目使用了一些C++新特性，需要CXX-20标准以及新版本的编译器提供必要支持**。

### Verilator

本项目使用的Verilator必须采用源码构建的方式安装，因为verilator在CMake项目中集成需要使用`VERILATOR_ROOT`来索引`include`和`bin`目录以完成编译流程，因此需要先卸载已安装的verilator：

- 若是使用apt安装的verilator: `sudo apt remove verilator`
- 若是使用源码`sudo make install`安装的方式，使用：`sudo make uninstall`

本项目建议在用户在主目录下建立`softwares`目录，而后在该目录下下载安装verilator

```sh
mkdir -p ~/sofware && cd ~/software && git clone https://github.com/verilator/verilator && cd verilator
autoconf && ./configure && make -j
# if use zsh
echo "export VERILATOR_ROOT=${HOME}/softwares/verilator" >> ~/.zshrc
echo "export PATH=${VERILATOR_ROOT}/bin:$PATH" >> ~/.zshrc
# if use bash
echo "export VERILATOR_ROOT=${HOME}/softwares/verilator" >> ~/.bashrc
echo "export PATH=${VERILATOR_ROOT}/bin:$PATH" >> ~/.bashrc
```

### Java JDK

使用sdkman管理java版本

```sh
curl -s "https://get.sdkman.io" | bash
sdk version
sdk update && sdk install java 21.0.1-tem
```

### Display Graphics

这一部分适用于不使用GUI虚拟机的Linux设备，若有使用gtkwave检视波形的需求请看这部分。

使用X11进行端口转发、图形显示

#### MacOS

mac上使用X11与Linux通信，需要：

1. 安装运行[XQuartz](https://www.xquartz.org)，设置 $\rightarrow$ 安全性 $\rightarrow$ 勾选允许从网络客户端链接
2. **运行`xhost +`**，允许所有链接
3. 使用-X连接remote或者在`~/.ssh/config`中`Host`下加入`ForwardX11 yes`
4. remote使用`DISPLAY`环境变量：`export DISPLAY=${HOSTNAME}:0`

#### Windows

Windows WSL已经[原生支持运行GUI应用](https://learn.microsoft.com/en-us/windows/wsl/tutorials/gui-apps)

windows上其他平台使用X11与Linux通信

[MacOS 教程](#macos)中第一步改为：

安装运行[VcXsrc](https://sourceforge.net/projects/vcxsrv/)

无需运行前述教程第二步，配置好后进行3/4步连接即可

## Installation(必做)

**注意：本项目所有命令除非特殊说明都在项目主目录下运行**

**注意：本项目已经集成进[OVIP-UT](https://gitee.com/yaozhicheng/OVIP-UT)**

打开终端，执行：

```sh
git clone https://gitee.com/yaozhicheng/OVIP-UT.git --recurse-submodules
```

确保`src/cpp`目录下`CMakeList.txt`中包含如下代码：

```cmake
add_definitions( -DUSE_THREADS=false )
add_definitions( -DBUGDEGREE=Degree::LOW )

add_executable(tb_memory tb_memory.cpp)
target_link_libraries(tb_memory mlvp-lib pthread)
if (${CMAKE_BUILD_TYPE} STREQUAL "Debug")
    verilate(tb_memory SOURCES ${PROJECT_SOURCE_DIR}/mlvp/design/Memory/memory.sv TOP_MODULE memory COVERAGE OPT_SLOW TRACE)
else ()
    verilate(tb_memory SOURCES ${PROJECT_SOURCE_DIR}/mlvp/design/Memory/memory.sv TOP_MODULE memory COVERAGE OPT_FAST TRACE)
endif ()
```

首先需要安装`mlvp-lib`，在`mlvp`主目录下执行`./scripts/build.sh install`，将会自动完成编译安装
