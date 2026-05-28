# AdrianMCPLab

freee会計と Claude Code を連携させた、会計仕訳自動化スキルのリポジトリです。

---

## 収録スキル

### `freee-ini.skill` — freee 会計自動化セットアップ

ほぼ空のフォルダーから、freee会計との連携パイプラインを **ワンセッションで構築・実行** するスキルです。

#### 主な機能

| ステップ | 内容 |
|----------|------|
| **Step 1** | freee から過去仕訳を取得し、会社固有の会計ルールを自動学習 |
| **Step 2** | `invoices/` に置いた発票画像を OCR 処理 → 仕訳データ（JSON）を生成 |
| **Step 3** | 税額・勘定科目を検証し、問題のないものだけ freee へバッチアップロード |

#### セットアップされるフォルダー構造

```
your-project/
├── CLAUDE.md                  ← Claude Code の行動規則 & 自動学習された会計ルール
├── .company_config.json       ← 会社ID・設定
├── prompts/
│   ├── 01_learn_style.md
│   ├── 02_ocr_upload.md
│   └── 03_verify_upload.md
├── scripts/
│   ├── run_pipeline.sh        ← 全ステップ一括実行
│   └── run_step.sh            ← 単ステップ実行
├── invoices/                  ← 発票画像を置くフォルダー
├── output/                    ← OCR結果・仕訳データの一時保存
└── logs/                      ← 実行ログ
```

#### 前提条件

- [Claude Code](https://claude.ai/code) がインストール済みであること
- [freee MCP](https://github.com/freee/freee-mcp) が設定・認証済みであること

#### 使い方

1. このリポジトリから `freee-ini.skill` をダウンロード
2. Claude Code のスキルとしてインストール
3. 任意の作業フォルダーで Claude Code を起動し、以下のように話しかける：

```
freeeの会計を自動化したい
```

スキルが自動的に起動し、freee への接続確認・会社選択・フォルダーセットアップを順に行います。

---

## ライセンス

MIT
