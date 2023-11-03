---
title: MVM文档 - 首页
summary: MVM Index
authors:
    - BlueSpace
date: 2023-11-01
---

{!README.md!}

**注意：本项目所有命令除非特殊说明都在MVM项目主目录下运行**
**注意：本项目已经集成进[OVIP-UT](https://gitee.com/yaozhicheng/OVIP-UT/blob/master/src/cpp/tb_memory.cpp)**

## Installation and Configuration

详细步骤及common issue请见[安装与配置章节](./prepare.md)，其中本项目安装部分为必做

快速安装：在项目根目录运行

```sh
./scripts/prepare.md
```

## Quick Start

前提：按照上一节完成环境安装与配置，详细说明见[Quick Start章节](./quickstart.md)

本项目由CMake构建，安装后在`MVM`目录下执行：

```sh
# build file
./bin/build.sh

# check raw system verilog file
cat design/Memory/memory.sv

# run test
./bin/mvm

# check total result
cat report/memory/total.info

# check coverage of system verilog loc
cat report/memory/memory.sv

# check vcd waveform
gtkwave log/memory/Driver0/memory.vcd
```

在以上步骤中我们完成了编译、验证目标查看、执行、结果查看，成功完成了一个简单的UT验证流程，获取到正确与否的验证结果和代码覆盖率报告。

若对本项目感兴趣并希望深入了解相关架构与设计，请继续阅读。

## Tutorial

教程参考[教程章节](./tutorial.md)

## Developer Guide

若想要参与开发，请查阅[开发者指南](./developer.md)

## API Reference

本项目使用doxygen构建基于注释的API查询的文档，请参阅[API文档](./doxygen/html/index.html)