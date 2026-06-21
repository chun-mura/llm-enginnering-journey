# フェーズ4: LangGraph / LangChain / Observability / Evals

> 2026 年時点で LangGraph は LangChain の「拡張」ではなく独立したオーケストレーションフレームワークとして確立している。
> 本フェーズでは LangGraph を主役に置き、LangChain は概観として抑える構成にしている。

クラウド + データ基盤 + TypeScript/Python の経験があるので、このフェーズはかなり速く進められるはずです。

---

## 4-1. LangGraph（主役）（2〜4 週間）

> LangChainが解決していた問題（プロバイダー差異吸収）は各社 SDK が自己解決した。
> 本番開発トレンドは「生の SDK（OpenAI SDK / Anthropic SDK）+ LangGraph」に移行している。

### 公式ドキュメント/リポジトリ

- 公式サイト: https://www.langchain.com/langgraph
- 公式 Docs: https://langchain-ai.github.io/langgraph/
- GitHub: https://github.com/langchain-ai/langgraph

### 学習の観点

- サイクリックグラフ（ループ・分岐・ステート管理）
- チェックポイントと LangGraph Studio（タイムトラベルデバッグ）
- マルチエージェントオーケストレーション（Supervisor / Swarm パターン）

### ハンズオン

- Python で「Plan → ToolUse → Review」ループを LangGraph で実装する
- LangGraph Studio でステート遷移を可視化し、失敗ノードを特定する
- TypeScript でも同じグラフを実装して API 経由で叩けるようにする

---

## 4-2. LangChain（概観）（1〜2 週間）

> LangChain は「フレームワーク」より「ツールキット」として使う位置づけに変化している。
> LangGraph を使うなら LangChain の概念は自然に身に付く。深追いは不要。

### 公式ドキュメント/リポジトリ

- 公式 Docs: https://docs.langchain.com
- GitHub: https://github.com/langchain-ai/langchain

### 押さえるだけでよいコンポーネント

- Models（LLM / ChatModel）、Prompts、Output Parsers
- Tools / Tool calling
- RAG（VectorStore / Retriever / Document Loader）

---

## 4-3. Observability（観測）（2〜3 週間）

> LangSmith と Langfuse は「どちらも学ぶ」より「用途で選ぶ」。
> LangChain スタックを使わないなら Langfuse（OSS・OpenTelemetry-native）が推奨。

### LangSmith（LangChain エコシステム中心）

- Docs: https://docs.langsmith.com
- GitHub (SDK): https://github.com/langchain-ai/langsmith-sdk

**使う場面**: LangGraph / LangChain を中心に組む場合。統合がシームレス。

### Langfuse（フレームワーク非依存・OSSセルフホスト）

- Docs: https://langfuse.com/docs
- GitHub (docs): https://github.com/langfuse/langfuse-docs

**使う場面**: 自前エージェント（FastAPI / Lambda）や LangChain 以外のスタックを使う場合。

### 学習の観点（共通）

- トレースモデル（traces / spans / events / metadata）
- プロンプト / エージェントのバージョニング
- ボトルネック可視化（どのツール呼び出しが遅いか・失敗しているか）

### ハンズオン

- フェーズ 3 のシングルエージェントを Langfuse に接続し、失敗トレースを収集する
- 「どのプロンプト/ツール呼び出し」がボトルネックかを可視化する

---

## 4-4. Evals（評価）（2〜3 週間）

> Evals は Observability とは別の関心事。「動いている」の観測ではなく「良い出力か」の判定。
> LangSmith の Evals 機能に加え、CI/CD 統合や詳細メトリクスに強いツールが台頭している。

### 主要 Evals ツール比較

| ツール | 特徴 | 向いているケース |
|--------|------|------------------|
| LangSmith | LangChain 統合・データセット管理 | LangGraph スタックで一気通貫 |
| Langfuse | OSS・LLM-as-a-judge・プロンプトバージョン管理 | セルフホスト・フレームワーク非依存 |
| Braintrust | CI/CD パイプライン統合に強い | 継続的評価・自動回帰テスト |
| DeepEval | 50+ 組み込みメトリクス（G-Eval・忠実度・ハルシネーション検出）・ローカル実行可 | 詳細なメトリクス評価・ローカル完結 |

### 読む

- Best LLM Evaluation Tools 2026: https://www.confident-ai.com/knowledge-base/compare/best-llm-evaluation-tools
- Braintrust 評価ツール比較: https://www.braintrust.dev/articles/best-llm-evaluation-tools-integrations-2025
- Langfuse vs LangSmith: https://www.zenml.io/blog/langfuse-vs-langsmith

### ハンズオン

- DeepEval でフェーズ 3 のエージェント出力を評価する（忠実度・ハルシネーション率を計測）
- Braintrust を CI に組み込み、プロンプト変更時に自動で eval を走らせる
