# CostQ — Cloud Cost Optimization with Amazon Q

[English](./README.md) | [日本語](./README.ja.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](#license)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

**CostQ** is an open-source project that demonstrates how to use **Amazon Q** to analyze AWS bills and generate **actionable cost optimization reports**. The project provides **Chinese/English/Japanese** **prompt templates**, **report templates**, and **execution handbooks**, helping you quickly understand cloud cost structures and optimization opportunities with Amazon Q.

## Why CostQ

* **Results-Oriented**: Executive summary → Optimization plan → Execution checklist.
* **Tri-lingual Support**: **Chinese / English / Japanese** prompts and reports.
* **Plug-and-Play Data**: Integrates with APIs such as Cost Explorer, Cost Optimization Hub, Compute Optimizer, SP/RI coverage & utilization, S3/EC2 monitoring metrics.

## Repository Structure

```
.
├─ prompts/       # Prompt templates for different roles
│  ├─ zh-CN/     
│  ├─ en/
│  └─ ja/
├─ reports/       # Cost analysis report templates
│  ├─ report.zh-CN.md   
│  ├─ report.en.md
│  └─ report.ja.md
├─ handbook/      # Amazon Q installation and execution handbook
│  ├─ runbook.zh-CN.md  
│  ├─ runbook.en.md
│  └─ runbook.ja.md
```

## Prerequisites

* **Cost Explorer** enabled.
* **Amazon Q CLI** installed and configured.

## Quick Start

1. **Prepare Amazon Q**: Follow [handbook/runbook.zh-CN.md](handbook/runbook.zh-CN.md) to create permissions and install Amazon Q.
2. **Choose a Language**: Use the `prompts/zh-CN` prompt template in **Amazon Q**.
3. **Generate Reports**: Ask Q to produce:
   * **Executive Report**: Cost trends, cost drivers, savings opportunities.

## Prompt Content Overview

* **Multi-dimensional Cost Overview**: Cost efficiency metrics + cost composition.
* **Intelligent Anomaly Detection & Root Cause Analysis**: Anomaly triggers + CloudTrail deep analysis.
* **Optimization Strategies Based on Cost Analysis**: Identify optimization potential + recommendations.
* **Actionable Cost Optimization Reports**

## Suggested Amazon Q Usage

* First generate an **executive summary report** → Then ask Q to **cite data evidence** for each conclusion.
* Next generate a **cost optimization report** → Require **owners**, **risk/rollback**, and **validation metrics**.

## Security & Privacy

* **Do not** submit raw bills, account IDs, or other sensitive information.
* Always anonymize before external sharing.
* This project has **no official affiliation with AWS**, for learning and collaboration only.

## Contributing

PRs are welcome! Please:

* Use Conventional Commits (e.g., `feat:`, `fix:`).
* Add sample/test data (anonymized).
* Keep prompts auditable and reproducible.

## License

[MIT](./LICENSE)
