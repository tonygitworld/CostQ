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
