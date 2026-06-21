「LLMエージェントエンジニア（仮）」向けロードマップとして整理します。 [note](https://note.com/noble_crane1635/n/n73100d30ea37)
「概念 → 小さく作る → 計測・改善 → プロダクション」を一気通貫で繋げる内容にしています。 [genai-career](https://www.genai-career.com/context-engineering/)

***

## 全体像（フェーズ設計）

1. フェーズ0: 前提知識の整理（LLM/エージェント全体像）
2. フェーズ1: プロンプト/コンテキストエンジニアリング
3. フェーズ2: ハーネス/ループエンジニアリング
4. フェーズ3: シングルエージェント設計
5. フェーズ4: LangChain / LangSmith / Langfuse 実務利用
6. フェーズ5: StrandsAgents とマルチエージェント・AWS 連携

各フェーズで「学ぶ → 手を動かす → 計測する → 小さく振り返る」を 2〜4 週間単位で回すイメージです。  

***

## フェーズ0: 前提知識（LLM/エージェントの全体像）

### 目的
- 「プロンプト/コンテキスト/ハーネス/エージェント」という用語群を 1 本のストーリーで理解する。  
- シングルエージェント vs マルチエージェントの設計判断軸を掴む。 [arxiv](https://arxiv.org/html/2504.05716v1)

### 読む/見る

- 記事: 「プロンプトからエージェントまで。AIを使いこなすための4つのステップ」  
  （プロンプト/コンテキスト/ハーネス/エージェントのレイヤ整理） [note](https://note.com/noble_crane1635/n/n73100d30ea37)
- 記事: コンテキスト/ハーネスの対比と定義を整理している Zenn 記事  
  [プロンプトエンジニアリング → コンテキスト → ハーネスの整理](https://zenn.dev/emuni/articles/7c1493a52a3569) [zenn](https://zenn.dev/emuni/articles/7c1493a52a3569)
- 概説: Google Cloud の AI エージェント解説（単一エージェントの定義） [cloud.google](https://cloud.google.com/discover/what-are-ai-agents?hl=ja)
- 概説: Dataiku の single-agent vs multi-agent のエンタープライズ視点の整理 [dataiku](https://www.dataiku.com/stories/blog/single-agent-vs-multi-agent-systems)
- 概説: シングルエージェントとマルチエージェントの特徴を整理した解説記事（日本語） [chowagiken.co](https://www.chowagiken.co.jp/future-studio/aiagent_singleagent_multiagent_1/)

### やること（1 週間）

- 自分なりの **レイヤー図** を 1 枚描く  
  - 対話レイヤ（プロンプト）  
  - 情報レイヤ（コンテキスト/RAG）  
  - 実行環境レイヤ（ハーネス/ループ）  
  - エージェントアーキテクチャ（シングル/マルチ）  
- その図を元に、既存の自分のプロダクト/業務をどのレイヤまでカバーしているか言語化しておく。  

***

## フェーズ1: プロンプト & コンテキストエンジニアリング

### 目的
- プロンプト単体の最適化から、「何をどう見せるか」まで含めた設計ができるようにする。 [shareuhack](https://www.shareuhack.com/ja/posts/context-engineering-guide-2026)

### 1-1. プロンプトエンジニアリング（2〜4 週間）

**読む**

- 解説記事: 3 ヶ月で学ぶプロンプトエンジニアリングロードマップ（日本語） [note](https://note.com/jux/n/n48e963834f23)
- 解説記事: 2025/2026 年向けのプロンプトエンジニアリング総論記事（ロードマップ付き） [kirekaku](https://kirekaku.com/438/)

**動画（英語でもよければ）**

- OpenAI / Anthropic / DeepLearning.AI などの「Prompt Engineering」入門コース（YouTube 上に多数）  
  （例）DeepLearning.AI “ChatGPT Prompt Engineering for Developers”（YouTube 探索を想定）  

**ハンズオン**

- ChatGPT / Claude / Gemini どれでもよいので、以下をテンプレ化  
  - Role Prompt + Style + Constraints を 3 パターン作る（例: コードレビュー、要件定義、SQL 生成）  
  - Few-shot プロンプトで「よくやる業務」を 3 つ自動化（例: PR サマリ生成など）  

***

### 1-2. コンテキストエンジニアリング（2〜4 週間）

**読む**

- 入門記事: 「コンテキストエンジニアリングとは？基本から実践まで」 [qiita](https://qiita.com/nogataka/items/4ec84d29055fbddca82f)
- 実践ガイド: 2026 年版コンテキストエンジニアリング完全ガイド（Write/Select/Compress/Isolate 戦略） [shareuhack](https://www.shareuhack.com/ja/posts/context-engineering-guide-2026)
- GitHub: Karpathy 系の Context Engineering リポジトリ（記事内で `davidkimai/Context-Engineering` が紹介） [shareuhack](https://www.shareuhack.com/ja/posts/context-engineering-guide-2026)

**ハンズオン**

- 自分の OSS or 社内リポジトリ 1 つを対象に  
  1. 単純な「長大コンテキスト 1 発プロンプト」  
  2. Write + Select（RAG/検索ベース）戦略  
  3. Compress 戦略（要約＋再プロンプト）  
  を実装して、コストと品質差を比較する。 [qiita](https://qiita.com/nogataka/items/4ec84d29055fbddca82f)

***

## フェーズ2: ハーネスエンジニアリング & ループエンジニアリング

### 目的
- 「モデルにどう聞くか」ではなく、「どういう環境・ループで走らせるか」を設計する能力を身につける。 [ai-kidou](https://ai-kidou.jp/loop-engineering-guide/)

### 2-1. ハーネスエンジニアリング（2〜4 週間）

**読む**

- 解説記事: ハーネスエンジニアリングとは何か（AIエージェントの品質を環境設計で上げる解説） [hexabase](https://www.hexabase.com/column/harness-engineering-langchain-52-to-66-improvement)
- 実践記: 自分のプロジェクトにハーネスエンジニアリングを導入した Qiita 記事 [qiita](https://qiita.com/nogataka/items/a8306067788798975fa7)
- 記事: プロンプト/コンテキスト/ハーネスの違いを 1 表で整理した記事 [zenn](https://zenn.dev/emuni/articles/7c1493a52a3569)

**ハンズオン**

- 既存の「コード生成エージェント」（Claude Code / Copilot 等）利用を想定し  
  - CLAUDE.md / CONTRIBUTING.md 的な **ハーネスファイル** を 50 行以内で作成する。 [note](https://note.com/anyoneanderson/n/n73ee45492532)
  - pre-commit + テスト実行を「Stop Hook」として必須化（PR 作成前に必ず通るゲート） [qiita](https://qiita.com/nogataka/items/a8306067788798975fa7)
  - エージェント失敗パターンが出るたびにルール or テストを追加する運用を 2〜4 週間続ける。 [qiita](https://qiita.com/nogataka/items/a8306067788798975fa7)

### 2-2. ループエンジニアリング（2〜3 週間）

**読む**

- 入門記事: 「Claude Fable 5 時代のループエンジニアリング入門」 [ai-kidou](https://ai-kidou.jp/loop-engineering-guide/)

**ハンズオン**

- 小さなタスク（例: ブログ生成、SQL 修正、ログ調査など）を対象に  
  1. 人間が毎回指示するワンショット運用  
  2. 「Plan → Do → Check → Fix」のループを、2 つの会話/エージェントで回す設計  
  を試し、成功率・時間・手戻りを簡単にメモしておく。 [hexabase](https://www.hexabase.com/column/harness-engineering-langchain-52-to-66-improvement)

***

## フェーズ3: シングルエージェント設計

### 目的
- シングルエージェントの設計パターンを体系化し、「どこまでを 1 体に任せるか」を判断できるようにする。 [iret](https://iret.media/194024)

### 読む

- 定義: Google Cloud による AI エージェント（単一エージェント）の定義 [cloud.google](https://cloud.google.com/discover/what-are-ai-agents?hl=ja)
- 解説: 日本語での Single Agent vs Multi Agent の整理記事 [chowagiken.co](https://www.chowagiken.co.jp/future-studio/aiagent_singleagent_multiagent_1/)
- 分析: Read-heavy/Multi vs Write-heavy/Single の設計指針を解説した英語記事 [zenn](https://zenn.dev/r_kaga/articles/ea7119d22d4d3c?locale=en)

### ハンズオン（2〜4 週間）

- ターゲット: 「Issue → 調査 → 修正案の生成 → PR テンプレ生成」までを 1 エージェントに担わせる。  
- 設計項目  
  - Profile（役割定義）  
  - Memory（短期/長期。会話履歴 vs 外部ストア）  
  - Tool セット（GitHub API / DB / HTTP / Shell など）  
  - 成功条件（テスト通過、CI 成功、diff の粒度）  
- Single エージェント構成で実装し、Multi にした場合どう分割するかもメモしておく。 [iret](https://iret.media/194024)

***

## フェーズ4: LangChain / LangSmith / Langfuse

クラウド + データ基盤 + TypeScript/Python の経験があるので、このフェーズはかなり速く進められるはずです。  

### 4-1. LangChain（2〜4 週間）

**公式ドキュメント/リポジトリ**

- 公式 Docs: [https://docs.langchain.com](https://docs.langchain.com) [docs.langchain](https://docs.langchain.com)
- 統合リファレンス: LangChain / LangGraph Python リファレンス [reference.langchain](https://reference.langchain.com/python/)
- GitHub: langchain-ai/langchain（エージェントフレームワークとしての位置づけ） [github](https://github.com/langchain-ai/langchain)

**学習の観点**

- 最低限押さえるコンポーネント  
  - Models（LLM / ChatModel）、Prompts、Output Parsers  
  - Tools / Tool calling  
  - RAG（VectorStore / Retriever / Document Loader）  
  - LangGraph を使ったループ・エージェントの制御（Workflow / State machine） [reference.langchain](https://reference.langchain.com/python/)

**ハンズオン**

- Python で  
  - シングルエージェント（ツール 2〜3 個 + 簡易メモリ）  
  - LangGraph で「Plan → ToolUse → Review」ループを 1 つ作成  
- TypeScript でも同じ構成を実装して API 経由で叩けるようにしておく。  

***

### 4-2. LangSmith（2〜3 週間）

**公式リソース**

- Docs: LangSmith 公式ドキュメント [docs.langsmith](https://docs.langsmith.com)
- GitHub: langsmith-docs（ドキュメントのソース） [github](https://github.com/langchain-ai/langsmith-docs)
- GitHub: langsmith-sdk（Python/JS SDK） [github](https://github.com/langchain-ai/langsmith-sdk)

**学習の観点**

- トレーシング（requests / spans / metadata） [docs.langchain](https://docs.langchain.com/langsmith/home.md)
- 評価（Evals）とデータセット管理 [docs.langchain](https://docs.langchain.com/langsmith/home.md)
- Prompt / Agent のバージョニングと A/B テスト [docs.langsmith](https://docs.langsmith.com)

**ハンズオン**

- フェーズ 3 のシングルエージェントを LangSmith に接続  
  - 失敗事例を含むトレースを収集  
  - ログから「どのプロンプト/コンテキスト/ツール呼び出し」がボトルネックかを可視化 [docs.langsmith](https://docs.langsmith.com)

***

### 4-3. Langfuse（2〜3 週間）

**公式リソース**

- Docs: [https://langfuse.com/docs](https://langfuse.com/docs) [langfuse](https://langfuse.com/docs)
- GitHub: langfuse-docs（OSS ドキュメントリポジトリ） [github](https://github.com/langfuse/langfuse-docs)
- Docs: Public API ドキュメント [langfuse](https://langfuse.com/docs/api)

**学習の観点**

- LangSmith との思想的な違い（OSS / 自前ホスト / API-first） [github](https://github.com/langfuse/langfuse-docs)
- トレースモデル（traces / spans / events / metadata） [langfuse](https://langfuse.com/docs)
- オフライン評価（datasets / experiments / evals） [langfuse](https://langfuse.com/changelog/2024-11-21-all-new-datasets-and-evals-documentation)

**ハンズオン**

- LangChain なしの「自前エージェント（FastAPI or Lambda）」に Langfuse SDK を組み込み  
  - OpenAI / Anthropic SDK → Langfuse middleware で計測  
  - Data pipeline（Redshift / Athena 等）と連携して、Langfuse ログを分析用に落とす [langfuse](https://langfuse.com/docs/api)

***

## フェーズ5: StrandsAgents & マルチエージェント + AWS

### 目的
- AWS 文脈に寄せつつ、StrandsAgents でモデル駆動エージェント開発の感覚を掴む。 [docs.aws.amazon](https://docs.aws.amazon.com/prescriptive-guidance/latest/agentic-ai-frameworks/strands-agents.html)

### リソース

- GitHub: StrandsAgents Python SDK [github](https://github.com/strands-agents/sdk-python)
- AWS Prescriptive Guidance: StrandsAgents の概要 [docs.aws.amazon](https://docs.aws.amazon.com/prescriptive-guidance/latest/agentic-ai-frameworks/strands-agents.html)
- ブログ/記事: StrandsAgents のマルチエージェント設計パターン解説 [dev.classmethod](https://dev.classmethod.jp/articles/strands-agents-multi-agent-design-patterns/)
- 動画: AWS Developers - “Building Intelligent Agents with Strands: A Hands-On Guide” [youtube](https://www.youtube.com/watch?v=TD2ihEBkdkY)

### ハンズオン（2〜4 週間）

- 「AWS 上の運用タスク」を題材に 2 パターン作成  
  1. **シングルエージェント**: CloudWatch Logs を見て特定のパターンを検出し、Slack 通知する  
  2. **マルチエージェント**:  
     - 監視エージェント（ログ/メトリクス監視）  
     - トリアージエージェント（影響度と優先度付け）  
     - 対応エージェント（オートリカバリ or Runbook 提案）  
- ここでフェーズ 2 の「ハーネス/ループ設計」とフェーズ 4 の「観測（Langfuse/LangSmith）」を統合する。 [dev.classmethod](https://dev.classmethod.jp/articles/strands-agents-multi-agent-design-patterns/)

***

## シングルエージェント / LangChain / StrandsAgents を並べて見る

| 項目 | シングルエージェント | LangChain / LangGraph | StrandsAgents |
|------|----------------------|------------------------|---------------|
| 役割 | 1 つの LLM が計画〜実行まで担当 [cloud.google](https://cloud.google.com/discover/what-are-ai-agents?hl=ja) | LLM アプリ/エージェント全体の OSS フレームワーク [github](https://github.com/langchain-ai/langchain) | AWS 連携に強いモデル駆動エージェント SDK [github](https://github.com/strands-agents/sdk-python) |
| 適したタスク | プロセスが明確・ツール少なめ・整合性重視 [chowagiken.co](https://www.chowagiken.co.jp/future-studio/aiagent_singleagent_multiagent_1/) | RAG、ツール連携、LangGraph での複雑なフロー [reference.langchain](https://reference.langchain.com/python/) | AWS サービス連携、自律運用ワークフロー [docs.aws.amazon](https://docs.aws.amazon.com/prescriptive-guidance/latest/agentic-ai-frameworks/strands-agents.html) |
| 強み | 実装・運用のシンプルさ、コンテキスト維持 [chowagiken.co](https://www.chowagiken.co.jp/future-studio/aiagent_singleagent_multiagent_1/) | OSS エコシステム、豊富なインテグレーション [github](https://github.com/langchain-ai/langchain) | AWS 公式サポート、マルチエージェント設計パターン [docs.aws.amazon](https://docs.aws.amazon.com/prescriptive-guidance/latest/agentic-ai-frameworks/strands-agents.html) |
| 弱み | 大規模/並列タスクには不向き [dataiku](https://www.dataiku.com/stories/blog/single-agent-vs-multi-agent-systems) | 設定・バージョン管理が複雑になりがち [github](https://github.com/langchain-ai/langchain) | エコシステムは LangChain より若い [github](https://github.com/strands-agents/sdk-python) |

***

## 読むべき順序のひとつの案（ざっくりタイムライン）

1. 週 1–2  
   - フェーズ0 の記事一式 + 図を 1 枚書く [dataiku](https://www.dataiku.com/stories/blog/single-agent-vs-multi-agent-systems)
2. 週 3–6  
   - プロンプトエンジニアリング記事 + コンテキスト入門記事 [kirekaku](https://kirekaku.com/438/)
   - 自分の業務プロンプトをテンプレ化  
3. 週 7–10  
   - ハーネス/ループ記事 + 自プロジェクトへの導入 [ai-kidou](https://ai-kidou.jp/loop-engineering-guide/)
4. 週 11–16  
   - LangChain 公式 Docs / LangGraph 概念 [docs.langchain](https://docs.langchain.com)
   - シングルエージェント + LangGraph ワークフロー実装  
5. 週 17–22  
   - LangSmith / Langfuse Docs [github](https://github.com/langfuse/langfuse-docs)
   - 既存エージェントにトレーシング + eval 導入  
6. 週 23–28  
   - StrandsAgents GitHub / AWS Docs / 動画 [zenn](https://zenn.dev/fusic/articles/8dd670c37a8d68)
   - AWS 上で単純なマルチエージェント運用パターンを構築  

***
