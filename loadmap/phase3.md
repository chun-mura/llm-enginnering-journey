# フェーズ3: シングルエージェント設計

## 目的

シングルエージェントの設計パターンを体系化し、「どこまでを 1 体に任せるか」を判断できるようにする。

## 読む

- [ ] 定義: Google Cloud による AI エージェント（単一エージェント）の定義  
  https://cloud.google.com/discover/what-are-ai-agents?hl=ja

- [ ] 解説: 日本語での Single Agent vs Multi Agent の整理記事  
  https://www.chowagiken.co.jp/future-studio/aiagent_singleagent_multiagent_1/

- [ ] 分析: Read-heavy/Multi vs Write-heavy/Single の設計指針を解説した英語記事  
  https://zenn.dev/r_kaga/articles/ea7119d22d4d3c?locale=en

- [ ] 解説: iret による AI エージェント設計の解説  
  https://iret.media/194024

## ハンズオン（2〜4 週間）

**ターゲット**: 「Issue → 調査 → 修正案の生成 → PR テンプレ生成」までを 1 エージェントに担わせる

### 設計項目

| 項目 | 内容 |
|------|------|
| Profile | 役割定義 |
| Memory | 短期/長期。会話履歴 vs 外部ストア |
| Tool セット | GitHub API / DB / HTTP / Shell など |
| 成功条件 | テスト通過、CI 成功、diff の粒度 |

- [ ] Single エージェント構成で実装する
- [ ] Multi にした場合どう分割するかもメモしておく

---

## MCP（Model Context Protocol）によるツール設計

> MCP は 2026 年時点で事実上の業界標準となっている（月次 SDK ダウンロード 9,700 万件、Linux Foundation 管理、OpenAI・Google・Microsoft 共同スポンサー）。
> エージェントのツール連携は MCP サーバー設計を中心に考えるのが現実的。

### 読む

- [ ] 公式ロードマップ: 2026 MCP Roadmap  
  https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/

- [ ] MCP の普及状況と採用事例  
  https://www.digitalapplied.com/blog/mcp-97-million-downloads-model-context-protocol-mainstream

### 設計観点

- [ ] **既存 MCP サーバーを探す**: 公開サーバー 1 万件超。自作前にまず探す
- [ ] **自作 MCP サーバー**: stdio / HTTP の 2 つのトランスポートを理解する
- [ ] **セキュリティ**: ツールの権限スコープを最小化。外部公開 MCP サーバーを使う際はサンドボックスを挟む

### ハンズオン

- [ ] フェーズ 3 のエージェントで利用するツールを MCP サーバーとして実装する
  - GitHub API / DB / HTTP などを各 1 つ MCP サーバー化する
- [ ] VS Code / Claude Code などから MCP サーバーに接続して動作を確認する

---

## Reasoning Models のモデルルーティング設計

> o3（OpenAI）・Claude Opus 4 などの推論モデルは高コスト・高レイテンシ。
> 全リクエストを推論モデルに流すのはアンチパターン。用途に応じたルーティングが必要。

### 読む

- [ ] 推論モデルのプロンプト戦略ガイド（o3, Claude Opus 4, Gemini, R1）  
  https://sureprompts.com/blog/ai-reasoning-models-prompting-complete-guide-2026

### ルーティング設計の目安

| リクエスト割合 | モデル tier | 用途例 |
|--------------|------------|--------|
| 85〜95% | Flash / Haiku 相当 | 分類、要約、定型応答 |
| 5〜15% | Reasoning Model | 複雑推論、コード生成、多段階計画 |

### ハンズオン

- [ ] タスクの種類（複雑度・出力の重要性）を分類するルーター関数を実装する
- [ ] コスト・精度・レイテンシをモデル tier 別に計測して判断基準を言語化する
