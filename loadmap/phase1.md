# フェーズ1: プロンプト & コンテキストエンジニアリング

## 目的

プロンプト単体の最適化から、「何をどう見せるか」まで含めた設計ができるようにする。

---

## 1-1. プロンプトエンジニアリング（2〜4 週間）

### 読む

- [ ] 解説記事: 3 ヶ月で学ぶプロンプトエンジニアリングロードマップ（日本語）
  https://note.com/jux/n/n48e963834f23

- [x] 解説記事: 2025/2026 年向けのプロンプトエンジニアリング総論記事（ロードマップ付き）
  https://kirekaku.com/438/

### 動画（英語でもよければ）

- [ ] OpenAI / Anthropic / DeepLearning.AI などの「Prompt Engineering」入門コース（YouTube 上に多数）
  - 例）DeepLearning.AI "ChatGPT Prompt Engineering for Developers"

### ハンズオン

- [ ] ChatGPT / Claude / Gemini どれでもよいので、以下をテンプレ化
  - Role Prompt + Style + Constraints を 3 パターン作る（例: コードレビュー、要件定義、SQL 生成）
  - Few-shot プロンプトで「よくやる業務」を 3 つ自動化（例: PR サマリ生成など）

---

## 1-2. コンテキストエンジニアリング（2〜4 週間）

### 読む

- [x] 入門記事: 「コンテキストエンジニアリングとは？基本から実践まで」  
  https://qiita.com/nogataka/items/4ec84d29055fbddca82f

- [ ] 実践ガイド: 2026 年版コンテキストエンジニアリング完全ガイド（Write/Select/Compress/Isolate 戦略）  
  https://www.shareuhack.com/ja/posts/context-engineering-guide-2026

- [ ] GitHub: Karpathy 系の Context Engineering リポジトリ（記事内で `davidkimai/Context-Engineering` が紹介）  
  https://www.shareuhack.com/ja/posts/context-engineering-guide-2026

### ハンズオン

自分の OSS or 社内リポジトリ 1 つを対象に、以下の 3 戦略を実装してコストと品質差を比較する：

1. 単純な「長大コンテキスト 1 発プロンプト」
2. Write + Select（RAG/検索ベース）戦略
3. Compress 戦略（要約＋再プロンプト）

---

## 1-3. Long Context 時代の RAG 設計（1〜2 週間）

> 2026 年時点で主要モデルの標準コンテキストは 128k〜2M tokens に到達している。
> 「RAG は不要」論が出ているが、実測では丸ごと投入は RAG より精度 67% 低下・コスト 94% 増。
> **ハイブリッド戦略が現時点のベストプラクティス**。

### 読む

- [ ] フレームワーク: 1M Context Windows のトラップと RAG vs Long Context の判断基準  
  https://www.keepmyprompts.com/en/blog/1m-context-windows-trap-rag-decision-framework

- [ ] 本番判断軸: Long-Context Models vs. RAG — プロダクション向け意思決定フレームワーク  
  https://tianpan.co/blog/2026-04-09-long-context-vs-rag-production-decision-framework

### 判断基準（使い分けの目安）

| ケース | 推奨 |
|--------|------|
| コーパスがコンテキスト上限超 | RAG |
| データが頻繁に更新される | RAG |
| レイテンシ重視 | RAG |
| 複数ドキュメントの横断推論が必要 | RAG + Long Context ハイブリッド |
| ドキュメントが少量・静的 | Long Context 直接投入 |

### ハンズオン

- RAG のみ、Long Context のみ、ハイブリッドの 3 パターンでコスト・精度・レイテンシを計測する
- ベクターDB の選定も合わせて行う（pgvector / Qdrant / Pinecone から 1 つ選んで比較）
