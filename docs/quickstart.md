---
title: MVM文档 - 快速上手
summary: MVM Quick Start
authors:
    - BlueSpace
date: 2023-11-01
---

# MVM快速上手

本项目由CMake构建，安装后在`MVM`目录下执行：

```sh
# build file
./bin/build.sh

# check raw system verilog file
cat src/MCVPack/BareDut/Memory/memory.sv

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