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
├─ reports/
│  ├─ report.ja.md
│  ├─ report.en.md
│  └─ report.zh-CN.md
├─ handbook/
│  ├─ runbook.ja.md
│  ├─ runbook.en.md
│  └─ runbook.zh-CN.md
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
