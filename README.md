# CostQ
================================

Use Amazon Q for Cloud Cost Optimization

* `README.md`（英文，默认）
* `README.zh-CN.md`（中文）
* `README.ja.md`（日文）

---

## `README.md` (English – default)

# CostQ — Use Amazon Q for Cloud Cost Optimization

[中文](./README.zh-CN.md) | [日本語](./README.ja.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](#license)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

**CostQ** is an open-source project that shows how to leverage **Amazon Q** to analyze AWS spend and drive **actionable cost optimization**. It ships battle-tested **prompts** (Chinese / English / Japanese), **report templates** per language, and an **execution runbook** so teams can produce C-level summaries and engineering playbooks in minutes.

## Why CostQ

* **Outcome-focused**: From executive summary → optimization plan → execution checklist.
* **Multilingual**: Prompts & reports in **EN / 中文 / 日本語**.
* **Repeatable**: Opinionated folder structure & CI to generate reports.
* **Pluggable data**: Works with Cost Explorer exports, CUR slices, Compute Optimizer, SP/RI utilization reports, S3/EC2 metrics, etc.

## Repository Structure

```
.
├─ prompts/
│  ├─ en/        # English prompts (C-level, FinOps, Engineering)
│  ├─ zh-CN/     # Chinese prompts
│  └─ ja/        # Japanese prompts
├─ templates/
│  ├─ report.en.md
│  ├─ report.zh-CN.md
│  └─ report.ja.md
├─ handbook/
│  ├─ runbook.en.md
│  ├─ runbook.zh-CN.md
│  └─ runbook.ja.md
├─ data/         # Place Cost Explorer CSV, CUR slices, exports, etc.
├─ scripts/
│  └─ generate_report.py   # Render language-specific reports (MD/PDF)
├─ examples/
│  └─ sample_inputs/       # Redacted example inputs
└─ .github/workflows/
   └─ generate-report.yml  # Optional CI to build artifacts
```

## Prerequisites

* AWS account(s) with Cost Explorer enabled; optional **CUR** (Cost & Usage Report).
* Access to **Amazon Q** (Developer/Business).
* Python 3.10+ if you plan to use the local `scripts/generate_report.py`.

## Quick Start

1. **Prepare data**
   Export CSV from Cost Explorer and (optionally) Compute Optimizer, SP/RI coverage & utilization.
2. **Pick a language**
   Use `prompts/en` (or `zh-CN`, `ja`) prompts in **Amazon Q**, attach relevant CSV (redacted if needed).
3. **Generate a draft**
   Ask Amazon Q to:

   * Produce a **C-level summary** (cost trends, key drivers, savings potential).
   * Propose a **30/60/90-day plan** (SP/RI coverage, rightsizing, storage lifecycle, data transfer).
   * Output an **engineering runbook** (owners, steps, metrics).
4. **Render a report** (optional, local)

   ```bash
   python scripts/generate_report.py \
     --lang en \
     --inputs data/cost_explorer_*.csv data/sp_ri_*.csv \
     --template templates/report.en.md \
     --out out/CostQ-Report.en.md --pdf
   ```

## What’s Inside (Prompts Overview)

* **C-Level Brief**: 1-page trend + 3 key drivers + quantified savings.
* **FinOps Deep Dive**: Cost Categories, tagging health, SP/RI coverage & utilization, anomaly highlights.
* **Engineering Playbook**: EC2/ASG rightsizing, GP2→GP3, S3 lifecycle & IA/Glacier, NAT egress, inter-AZ DT, CloudFront caching, RDS storage & IOPS, EKS nodegroup mix (On-Demand/Spot), autoscaling guardrails.

## Suggested Workflow with Amazon Q

* Start with **C-Level** prompt → validate numbers → ask Q to **justify** each top driver with dataset references.
* Move to **FinOps** prompt → request **coverage/utilization targets** and **sensitivity analysis**.
* Generate **Runbook** → ask for **owner matrix**, **risk/rollback**, and **verification steps**.

## Automation (Optional)

* **GitHub Actions** builds MD/PDF report artifacts on each push to `main` or on tag.
* Use repository secrets to avoid committing sensitive data.

## Roadmap

* ☑ Multilingual prompts (EN/zh/ja)
* ☐ Templated dashboards (Markdown → HTML/PDF)
* ☐ CUR transformer snippets
* ☐ Sample Cost Categories & Tagging policy kit

## Security & Privacy

* **Never** commit raw billing data or account IDs.
* Redact datasets before sharing.
* This project is **community-driven** and **not affiliated with AWS**.

## Contributing

PRs welcome! Please:

* Use Conventional Commits (`feat:`, `fix:`…).
* Add tests or example inputs where applicable.
* Keep prompts deterministic and auditable.

## License

[MIT](./LICENSE)

---

## `README.zh-CN.md`（简体中文）

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
├─ templates/
│  ├─ report.zh-CN.md
│  ├─ report.en.md
│  └─ report.ja.md
├─ handbook/
│  ├─ runbook.zh-CN.md
│  ├─ runbook.en.md
│  └─ runbook.ja.md
├─ data/
├─ scripts/
│  └─ generate_report.py
├─ examples/
└─ .github/workflows/
   └─ generate-report.yml
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

---

## `README.ja.md`（日本語）

# CostQ — Amazon Q でクラウドコスト最適化

[English](./README.md) | [中文](./README.zh-CN.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](#ライセンス)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#コントリビュート)

**CostQ** は **Amazon Q** を活用して AWS コストを分析し、**実行可能な最適化**へつなげるオープンソースです。**英語／中国語／日本語**の **プロンプト**、**レポート雛形**、**実行ランブック**を提供し、C-レベル向け要約からエンジニアの手順まで一気通貫で生成できます。

## 特長

* **成果志向**：エグゼクティブサマリ → 最適化計画 → 実行チェックリスト。
* **多言語**：**EN / 中文 / 日本語**。
* **再現性**：標準化ディレクトリ & CI によるレポート生成。
* **データ即応**：Cost Explorer、CUR、Compute Optimizer、SP/RI、S3/EC2 指標などに対応。

## リポジトリ構成

```
.
├─ prompts/
│  ├─ ja/        # 日本語プロンプト（経営・FinOps・実行手順）
│  ├─ en/
│  └─ zh-CN/
├─ templates/
│  ├─ report.ja.md
│  ├─ report.en.md
│  └─ report.zh-CN.md
├─ handbook/
│  ├─ runbook.ja.md
│  ├─ runbook.en.md
│  └─ runbook.zh-CN.md
├─ data/
├─ scripts/
│  └─ generate_report.py
├─ examples/
└─ .github/workflows/
   └─ generate-report.yml
```

## 前提

* **Cost Explorer** を有効化（可能なら **CUR** も）。
* **Amazon Q**（Developer/Business）が利用可能。
* ローカル生成の場合は **Python 3.10+**。

## はじめかた

1. **データ準備**：Cost Explorer / Compute Optimizer などから CSV をエクスポート（必要ならマスキング）。
2. **言語選択**：**Amazon Q** で `prompts/ja` を使用し、CSV を添付。
3. **ドラフト生成**：Q に以下を依頼

   * **経営向け 1 ページ要約**（トレンド、主要ドライバ、節約見込み）。
   * **30/60/90 日計画**（SP/RI、リサイズ、ストレージ階層化、データ転送料）。
   * **実行ランブック**（担当、手順、検証ポイント、ロールバック）。
4. **レポート生成（任意／ローカル）**

   ```bash
   python scripts/generate_report.py \
     --lang ja \
     --inputs data/cost_explorer_*.csv data/sp_ri_*.csv \
     --template templates/report.ja.md \
     --out out/CostQ-Report.ja.md --pdf
   ```

## プロンプト内容（概要）

* **C-レベル向け要約**：トップ3ドライバ＋節約試算＋意思決定ポイント。
* **FinOps 分析**：Cost Categories、タグ健全性、SP/RI のカバレッジ＆利用率、異常検知。
* **実行手順**：EC2/ASG リサイズ、GP2→GP3、S3 ライフサイクル／Glacier、NAT／AZ 間転送、CloudFront キャッシュ、RDS 容量・IOPS、EKS ノードグループ（On-Demand/Spot）、スケーリングのガードレール。

## Amazon Q の活用パターン

* まず **経営要約** → 各結論の**根拠データ**を Q に提示させる。
* 次に **FinOps 深掘り** → **目標値（カバレッジ／利用率）**と**感度分析**を要求。
* **ランブック** → **責任マトリクス**、**リスク／ロールバック**、**検証指標**を明確化。

## 自動化（任意）

* **GitHub Actions** で MD/PDF をビルド。
* 機密データはコミットせず、リポジトリシークレットを使用。

## ロードマップ

* ☑ 多言語プロンプト
* ☐ レポート HTML/PDF テンプレート
* ☐ CUR 変換スニペット
* ☐ Cost Categories／タグ運用キット

## セキュリティとプライバシー

* 元データやアカウント ID は **コミット禁止**。
* 外部共有前に必ず匿名化。
* 本プロジェクトは AWS **非公式**です。

## コントリビュート

歓迎します！

* Conventional Commits を推奨。
* 例やテストデータ（匿名化済み）を追加。
* プロンプトは再現性と監査性を重視。

## ライセンス

[MIT](./LICENSE)
