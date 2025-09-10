# CostQ — 用 Amazon Q 做云成本优化

[English](./README.md) | [日本語](./README.ja.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](#许可)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#参与共建)

**CostQ** 是一个开源项目，演示如何使用 **Amazon Q** 分析 AWS 账单并产出**可执行的成本优化报告**。项目提供 **中/英/日** 三语的 **Prompt 模板**、**报告模板**和**执行手册**，帮助你使用AmazonQ 快速了解云成本结构以及优化空间。

## 为什么是 CostQ

* **结果导向**：高层摘要 → 优化计划 → 执行清单。
* **三语支持**：**中文 / 英文 / 日文** Prompt 与报告。
* **数据即插即用**：对接 Cost Explorer、Cost Optimization Hub、Compute Optimizer、SP/RI 覆盖与利用率、S3/EC2 监控指标等 API。

## 仓库结构

```
.
├─ prompts/       # 面向不同角色的提示词模板
│  ├─ zh-CN/     
│  ├─ en/
│  └─ ja/
├─ reports/       # 成本分析报告模板
│  ├─ report.zh-CN.md   
│  ├─ report.en.md
│  └─ report.ja.md
├─ handbook/      # AmazonQ 安装和执行手册
│  ├─ runbook.zh-CN.md  
│  ├─ runbook.en.md
│  └─ runbook.ja.md
```

## 前置条件

* 已开启 **Cost Explorer**。
* 安装配置 **Amazon Q CLI**。

## 快速开始

1. **准备Amazon Q**： 按照[handbook/runbook.zh-CN.md](handbook/runbook.zh-CN.md)的操作指南创建相关权限并安装Amazon Q，为接下来做好准备。
2. **选择语言**：在 **Amazon Q** 中使用 `prompts/zh-CN` 的 Prompt 模板。
3. **生成报告**：让 Q 产出
   * **管理层报告**：成本趋势、成本驱动因素、节省空间等。

## Prompt 内容概览

* **多维度成本概览**：成本效率指标 + 成本构成概览。
* **智能异常检测与根因分析**：异常检测触发条件 + CloudTrail深度分析。
* **基于成本本分析的优化策略**：是否存在成本优化空间 + 优化建议。
* **可执行的成本优化报告**

## 建议的 Amazon Q 使用法

* 先出 **管理层摘要报告** → 追问让 Q **引用数据佐证**每个结论。
* 再做 **成本优化报告** → 要求 **责任人**、**风险/回滚**、**验证指标**等。

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

