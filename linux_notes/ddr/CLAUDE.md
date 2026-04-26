# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 仓库概述

这是一个 **DDR 内存技术学习笔记** 集合，非软件项目。所有内容均为 Markdown 文档，无需编译、测试或运行。

## 文件结构

| 文件 | 内容 |
|------|------|
| `ddr.md` | 核心学习笔记：SDRAM 内部架构（Bank/Row/Column/Cell）、容量计算、DIMM 模组位宽概念、时序参数（tRCD, tRC, CL, tRP, tRAS）、DDR 各代次对比 |
| `IMX6ULL_section35_1_4.md` | i.MX 6ULL MMDC（多模式 DDR 控制器）参考手册英文原版 |
| `IMX6ULL_section35_1_4_双语.md` | 同上章节的中英双语版本 |
| `4Gb_DDR3_merged.md` | Micron DDR3L SDRAM 数据手册（MT41K 系列，4Gb），英文 |
| `JESD79-3D_merged.md` | JEDEC DDR3 标准规范（JESD79-3D），英文 |
| `JESD79-3D_merged_中文.md` | JEDEC DDR3 标准规范的中文翻译 |
| `MinerU_markdown_SM41J256M16M_*.md` | 国微电子 SM41J256M16M 4Gb DDR3 产品手册，中文 |
| `MinerU_markdown_终极内存技术指南_*.md` | 终极内存技术指南，中文 | **低优先级参考**——年代较久远的爱好者撰写文章，部分概念（如 P-Bank、北桥芯片、传统单通道架构）已过时，与现代 DDR3/DDR4 语境不完全适用。仅作辅助理解，不作为权威依据。 |

## 参考资料优先级

- **第一优先级**：JEDEC 标准（JESD79-3D）、芯片数据手册（Micron MT41K、国微电子 SM41J256M16M）、i.MX 6ULL 官方参考手册——这些是权威技术文档
- **第二优先级**：`ddr.md` 学习笔记——用户自己整理的知识体系
- **低优先级**：《终极内存技术指南》——历史爱好者文章，部分术语和架构描述已过时（如北桥概念、P-Bank/Rank 混用等），仅供参考，不作为知识判定依据

## 使用须知

- 所有文件为独立 Markdown 文档，直接阅读/编辑即可
- 文件通过 MinerU（PDF 转 Markdown 工具）提取，部分格式可能存在瑕疵（如 LaTeX 公式、HTML 表格），编辑时注意清理
- 新增或修改笔记时，保持现有的中英双语风格（如适用）
