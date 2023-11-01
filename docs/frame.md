---
title: MVM文档 - 框架
summary: MVM Framework
authors:
    - BlueSpace
date: 2023-11-01
---

# MVM Framework and Project Structure

MVM

```txt
.
|-- assets
|   `-- images
|-- bin
|-- config
|-- data
|-- doc
|   |-- mvm
|   |   `-- docs
|   `-- mvm-doc
|       `-- docs
|           `-- img
|-- include
|   |-- Config
|   |-- Database
|   |-- Driver
|   |-- Library
|   |-- MCVPack
|   |   `-- BareDut
|   |       |-- Memory
|   |       `-- Mux
|   |-- RefPack
|   |   |-- Memory
|   |   `-- Mux
|   |-- Reporter
|   |-- Sequencer
|   |-- Spreader
|   `-- Transaction
|-- log
|   `-- memory
|       |-- Driver0
|       |-- Driver1
|       |-- Driver2
|       `-- Driver3
|-- report
|   `-- memory
|-- scripts
|-- src
|   |-- Config
|   |-- Database
|   |-- Driver
|   |-- Library
|   |-- MCVPack
|   |   `-- BareDut
|   |       |-- Memory
|   |       `-- Mux
|   |-- RefPack
|   |   |-- Memory
|   |   `-- Mux
|   |-- Reporter
|   |-- Sequencer
|   |-- Spreader
|   `-- Transaction
|-- tests
|-- third-party
|   `-- include
|-- tmp
|   `-- example-systemverilog
|       |-- logs
|       |   `-- annotated
|       |-- logs1
|       |   `-- annotated
|       |-- newlog
|       `-- obj_dir
`-- tools
    `-- TestGenerator
        |-- include
        `-- src
            |-- cpp
            |-- golang
            |-- java
            `-- python
```