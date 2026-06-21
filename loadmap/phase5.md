# フェーズ5: StrandsAgents & マルチエージェント + AWS

## 目的

AWS 文脈に寄せつつ、StrandsAgents でモデル駆動エージェント開発の感覚を掴む。
マルチエージェント間通信のプロトコル標準（MCP / A2A）を理解し、本番設計に適用できるようにする。

## リソース

- GitHub: StrandsAgents Python SDK  
  https://github.com/strands-agents/sdk-python

- AWS Prescriptive Guidance: StrandsAgents の概要  
  https://docs.aws.amazon.com/prescriptive-guidance/latest/agentic-ai-frameworks/strands-agents.html

- ブログ/記事: StrandsAgents のマルチエージェント設計パターン解説  
  https://dev.classmethod.jp/articles/strands-agents-multi-agent-design-patterns/

- 動画: AWS Developers - "Building Intelligent Agents with Strands: A Hands-On Guide"  
  https://www.youtube.com/watch?v=TD2ihEBkdkY

- AWS Open Source Blog: Strands Agents 1.0 リリースノート（本番稼働事例・新機能）  
  https://aws.amazon.com/blogs/opensource/introducing-strands-agents-1-0-production-ready-multi-agent-orchestration-made-simple/

---

## A2A（Agent-to-Agent）プロトコル

> A2A は「エージェント↔エージェント」通信の標準プロトコル。
> Google 発→Linux Foundation 管理、150以上の組織が採用。StrandsAgents 1.0 にも統合済み。
> MCP が「エージェント↔ツール」の標準なら、A2A は「エージェント↔エージェント」の標準。

### 読む

- A2A Protocol v1 解説（エージェント間通信の仕組み）  
  https://medium.com/@richardhightower/a2a-protocol-v1-2026-how-ai-agents-actually-talk-to-each-other-c500079bca73

- A2A プロトコル採用状況（150 組織・主要クラウドプラットフォーム統合）  
  https://www.prnewswire.com/news-releases/a2a-protocol-surpasses-150-organizations-lands-in-major-cloud-platforms-and-sees-enterprise-production-use-in-first-year-302737641.html

### 設計観点

- JSON-RPC 2.0 over HTTPS でタスク委譲・ケイパビリティ共有・コンテキスト保持を定義
- MCP（ツール連携）と A2A（エージェント間通信）を組み合わせてアーキテクチャを設計する

---

## エージェント SDK 比較（フレームワーク選定）

> AWS 以外のコンテキストでも判断できるよう、主要 SDK のポジショニングを押さえておく。

| SDK | 特徴 | 向いているケース |
|-----|------|-----------------|
| AWS Strands | AWS Bedrock 統合・A2A 対応・本番実績あり | AWS エコシステム中心 |
| LangGraph | 最大本番実績・ステートフルグラフ・タイムトラベルデバッグ | 複雑な状態管理・大企業採用 |
| OpenAI Agents SDK | 軽量・Python-first・モデル切り替え可 | OpenAI 中心の小〜中規模エージェント |
| Google ADK | Python/TS/Java/Go 対応・フルプラットフォーム | GCP 連携・マルチ言語 |
| CrewAI | ロールベース・プロトタイプ高速 | POC・役割ベースのチームワークフロー |

### 読む

- AI Agent Frameworks 2026 比較: https://www.morphllm.com/ai-agent-framework
- OpenAI Agents SDK / Google ADK / Claude Agents SDK 比較:  
  https://composio.dev/content/claude-agents-sdk-vs-openai-agents-sdk-vs-google-adk

---

## ハンズオン（2〜4 週間）

「AWS 上の運用タスク」を題材に 2 パターン作成する：

### パターン 1: シングルエージェント

CloudWatch Logs を見て特定のパターンを検出し、Slack 通知する

### パターン 2: マルチエージェント（A2A プロトコル使用）

| エージェント | 役割 |
|-------------|------|
| 監視エージェント | ログ/メトリクス監視 |
| トリアージエージェント | 影響度と優先度付け |
| 対応エージェント | オートリカバリ or Runbook 提案 |

- エージェント間通信に A2A プロトコルを使用する
- 各エージェントのツール連携は MCP サーバーとして実装する

### 統合ポイント

フェーズ 2 の「ハーネス/ループ設計」とフェーズ 4 の「観測（Langfuse/LangSmith）・Evals（DeepEval/Braintrust）」をここで統合する。
