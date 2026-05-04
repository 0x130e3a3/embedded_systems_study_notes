# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个 **嵌入式系统学习笔记** 仓库，当前主要在 `linux_notes/ddr/` 目录下通过 AI 辅助学习 DDR 内存知识并撰写知识总结文档。本项目非代码项目，而是 Markdown 文档项目。

## 项目结构

```
embedded_system_study_notes/       ← git 根目录
── readme.md
├── linux_notes/
│   ├── ddr/                       ← 当前主要工作目录
│   │   ├── 01_ddr_theory.md                ← 第一部分：DDR相关理论知识（第1-10章）
│   │   ├── 02_ddr_chip_analysis.md         ← 第二部分：具体DDR芯片分析（第11章+）
│   │   ├── 03_controller_and_debug.md      ← 第三部分：控制器分析与实战调试（第12-13章+）
│   │   ├── CLAUDE.md                       ← 本文件，项目指引
│   │   ├── image_*.png                     ← 框图/截图等图片资源
│   │   └── references/                     ← 参考资料目录
│   │       ├── JESD79-3D_merged.md               ← JEDEC DDR3 标准（英文）
│   │       ├── JESD79-3D_merged_中文.md          ← JEDEC DDR3 标准（中文翻译）
│   │       ├── 4Gb_DDR3_merged.md                ← Micron DDR3 数据手册
│   │       ├── MinerU_markdown_SM41J256M16M.md   ← 国微电子 DDR3 数据手册
│   │       ├── MinerU_markdown_IMX6ULL参考手册.md ← i.MX6ULL 参考手册
│   │       ├── 第35章-MMDC翻译.md                 ← i.MX6ULL MMDC 控制器章节翻译
│   │       ├── MinerU_markdown_终极内存技术指南.md ← 内存技术综合指南
│   │       └── MinerU_markdown_【正点原子】...   ← 正点原子开发指南
│   ├── debug/ gpio/ i2c/ lock/ mtd/ pinctl/ power/ devicetree/
│   └── clang_notes/
├── mineru/                        ← MinerU 文档处理工具相关
└── .git/
```

## 文档说明

| 文档 | 内容 | 更新频率 |
|------|------|---------|
| `01_ddr_theory.md` | DDR 基础理论：概念、芯片组织结构、各代演进、信号与时序 | 稳定，很少改动 |
| `02_ddr_chip_analysis.md` | 具体芯片规格解读与数据手册分析 | 持续增加新芯片 |
| `03_controller_and_debug.md` | SoC 内存控制器架构与 DDR 初始化调试 | 持续增加新 SoC/控制器 |

## 参考资料优先级

参考资料按权威性分级，编写笔记时出现矛盾以高优先级为准（路径相对于 `linux_notes/ddr/references/`）：

| 优先级 | 类型 | 文件 | 说明 |
|--------|------|------|------|
| **P0** | JEDEC 官方标准 | `JESD79-3D_merged*.md` | 最高权威，行业标准 |
| **P1** | 芯片数据手册 (Datasheet) | `4Gb_DDR3_merged.md`, `MinerU_markdown_SM41J256M16M.md` | 厂商官方数据，可靠 |
| **P2** | 芯片参考手册 (Reference Manual) | `MinerU_markdown_IMX6ULL参考手册.md`, `第35章-MMDC翻译.md` | 厂商官方手册 |
| **P3** | 第三方技术书籍/指南 | `MinerU_markdown_终极内存技术指南.md` | 内容较全面，但可能存在过时或不准确之处 |
| **P4** | 第三方开发教程 | `MinerU_markdown_【正点原子】I.MX6U嵌入式Linux驱动开发指南V2.0.1.md` | 实践参考，权威性最低，可能过时或有误 |

**处理原则**：
- 优先引用 P0/P1 资料的内容
- P3/P4 资料与 P0/P1/P2 矛盾时，以 P0/P1/P2 为准
- 所有结论尽量给出参考资料出处以便追溯
