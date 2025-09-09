# CostQ — 用 Amazon Q 做云成本优化

[English](./README.md) | [日本語](./README.ja.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](#许可)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#参与共建)

**CostQ** 是一个开源项目，演示如何使用 **Amazon Q** 分析 AWS 账单并产出**可执行的成本优化方案**。项目提供 **中/英/日** 三语的 **Prompt 模板**、**报告模板**和**执行手册**，帮助你快速生成领导可读的摘要与工程落地指南。

## 为什么是 CostQ

* **结果导向**：从高层摘要 → 优化计划 → 执行清单。
* **三语支持**：**中文 / 英文 / 日文** Prompt 与报告。
* **可复用**：规范化目录与 CI 产物生成。
* **数据即插即用**：支持 Cost Explorer 导出、CUR 切片、Compute Optimizer、SP/RI 覆盖与利用率、S3/EC2 指标等。

## 仓库结构

```
.
├─ prompts/
│  ├─ zh-CN/     # 中文 Prompt（管理层/FinOps/工程落地）
│  ├─ en/
│  └─ ja/
├─ reports/
│  ├─ report.zh-CN.md
│  ├─ report.en.md
│  └─ report.ja.md
├─ handbook/
│  ├─ runbook.zh-CN.md
│  ├─ runbook.en.md
│  └─ runbook.ja.md
```

## 前置条件

* 已开启 **Cost Explorer**（建议启用 **CUR**）。
* 可使用 **Amazon Q**（Developer/Business）。
* 若本地渲染报告：Python 3.10+。

## 快速开始

1. **准备数据**：从 Cost Explorer/Compute Optimizer 导出 CSV（必要时打码/脱敏）。
2. **选择语言**：在 **Amazon Q** 中使用 `prompts/zh-CN` 的 Prompt，并附上数据文件。
3. **生成初稿**：让 Q 产出

   * **管理层摘要**：趋势、成本驱动、可落地节省空间（量化）。
   * **30/60/90 天优化计划**：SP/RI、规格与副本数调整、存储分层、数据传输等。
   * **工程执行手册**：责任人、步骤、验证点与回滚。
4. **渲染报告（可选，本地）**

   ```bash
   python scripts/generate_report.py \
     --lang zh-CN \
     --inputs data/cost_explorer_*.csv data/sp_ri_*.csv \
     --template templates/report.zh-CN.md \
     --out out/CostQ-Report.zh-CN.md --pdf
   ```

## Prompt 内容概览

* **管理层 1 页报告**：3 大驱动 + 节省测算 + 决策建议。
* **FinOps 深挖**：Cost Categories、标签健康度、SP/RI 覆盖与利用率、异常消耗。
* **工程落地清单**：EC2/ASG 规格与副本、GP2→GP3、S3 生命周期/Glacier、NAT/跨可用区流量、CloudFront 命中率、RDS 存储与 IOPS、EKS 节点组 On-Demand/Spot 配比、HPA/CA 守护项。

## 建议的 Amazon Q 使用法

* 先出 **管理层摘要** → 追问让 Q **引用数据佐证**每个结论。
* 再做 **FinOps** → 要求 **目标覆盖/利用率** 与 **敏感性分析**。
* 生成 **执行手册** → 要求 **责任矩阵**、**风险/回滚**、**验证指标**。

## 自动化（可选）

* **GitHub Actions** 自动生成 Markdown/PDF 报告产物。
* 使用仓库密钥存放敏感变量，避免提交原始账单数据。

## 路线图

* ☑ 三语 Prompt
* ☐ 报告 HTML/PDF 模板
* ☐ CUR 转换示例
* ☐ 成本分类 & 标签策略样例

## 安全与隐私

* **不要**提交原始账单、账户 ID 等敏感信息。
* 对外分享前务必脱敏。
* 本项目与 AWS **无官方关联**，仅供学习交流。

## 参与共建

欢迎 PR！请：

* 使用 Conventional Commits（如 `feat:`、`fix:`）。
* 补充示例/测试数据（已脱敏）。
* 保持 Prompt 可审计、可复现。

## 许可

[MIT](./LICENSE)

