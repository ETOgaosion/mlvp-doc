---
title: MLVP文档 - 快速上手
summary: MLVP Quick Start
authors:
    - BlueSpace
date: 2023-11-01
---

# MLVP快速上手

## Memory案例

本项目由CMake构建，安装后在`MLVP`目录下执行：

```sh
# build file
./bin/build.sh

# check raw system verilog file
cat design/NutshellCache/nutshellcache.sv

# run test
./bin/mlvp

# check total result
cat report/cache/total.info

# check coverage of system verilog loc
cat report/cache/cache.sv

# check vcd waveform
gtkwave log/cache/Driver0/cache.vcd
```

在以上步骤中我们完成了编译、验证目标查看、执行、结果查看，成功完成了一个简单的UT验证流程，获取到正确与否的验证结果和代码覆盖率报告。

若对本项目感兴趣并希望深入了解相关架构与设计，请继续阅读。

## 自定义案例

### Prerequests

先完成Installation环节

### 实施

在OVIP-UT项目[templates/main.cpp](https://gitee.com/yaozhicheng/mlvp/blob/master/template/main.cpp)中添加实现，可参考现有实现，在OVIP-UT项目主目录执行：

```sh
./mlvp/scripts/build.sh
```

将完成tb目标的构建，执行`./build/bin/[target]`即可运行，在`log/report`目录下查看波形/覆盖率报告