# フェーズ2: ハーネスエンジニアリング & ループエンジニアリング

## 目的

「モデルにどう聞くか」ではなく、「どういう環境・ループで走らせるか」を設計する能力を身につける。

---

## 2-1. ハーネスエンジニアリング（2〜4 週間）

### 読む

- 解説記事: ハーネスエンジニアリングとは何か（AIエージェントの品質を環境設計で上げる解説）  
  https://www.hexabase.com/column/harness-engineering-langchain-52-to-66-improvement

- 実践記: 自分のプロジェクトにハーネスエンジニアリングを導入した Qiita 記事  
  https://qiita.com/nogataka/items/a8306067788798975fa7

- 記事: プロンプト/コンテキスト/ハーネスの違いを 1 表で整理した記事  
  https://zenn.dev/emuni/articles/7c1493a52a3569

### ハンズオン

既存の「コード生成エージェント」（Claude Code / Copilot 等）利用を想定して：

- CLAUDE.md / CONTRIBUTING.md 的な **ハーネスファイル** を 50 行以内で作成する
  - 参考: https://note.com/anyoneanderson/n/n73ee45492532
- pre-commit + テスト実行を「Stop Hook」として必須化（PR 作成前に必ず通るゲート）
- エージェント失敗パターンが出るたびにルール or テストを追加する運用を 2〜4 週間続ける

---

## 2-2. ループエンジニアリング（2〜3 週間）

### 読む

- 入門記事: 「Claude Fable 5 時代のループエンジニアリング入門」  
  https://ai-kidou.jp/loop-engineering-guide/

### ハンズオン

小さなタスク（例: ブログ生成、SQL 修正、ログ調査など）を対象に以下を比較し、成功率・時間・手戻りを簡単にメモしておく：

1. 人間が毎回指示するワンショット運用
2. 「Plan → Do → Check → Fix」のループを、2 つの会話/エージェントで回す設計
