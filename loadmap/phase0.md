# フェーズ0: 前提知識（LLM/エージェントの全体像）

## 目的

- 「プロンプト/コンテキスト/ハーネス/エージェント」という用語群を 1 本のストーリーで理解する
- シングルエージェント vs マルチエージェントの設計判断軸を掴む

## 読む/見る

- [x] 記事: 「プロンプトからエージェントまで。AIを使いこなすための4つのステップ」
  （プロンプト/コンテキスト/ハーネス/エージェントのレイヤ整理）
  https://note.com/noble_crane1635/n/n73100d30ea37

- [x] 記事: コンテキスト/ハーネスの対比と定義を整理している Zenn 記事
  https://zenn.dev/emuni/articles/7c1493a52a3569

- [x] 概説: Google Cloud の AI エージェント解説（単一エージェントの定義）
  https://cloud.google.com/discover/what-are-ai-agents?hl=ja

- [x] 概説: Dataiku の single-agent vs multi-agent のエンタープライズ視点の整理
  https://www.dataiku.com/stories/blog/single-agent-vs-multi-agent-systems

- [ ] 概説: シングルエージェントとマルチエージェントの特徴を整理した解説記事（日本語）
  https://www.chowagiken.co.jp/future-studio/aiagent_singleagent_multiagent_1/

## やること（1 週間）

- 自分なりの **レイヤー図** を 1 枚描く
  - 対話レイヤ（プロンプト）
  - 情報レイヤ（コンテキスト/RAG）
  - 実行環境レイヤ（ハーネス/ループ）
  - エージェントアーキテクチャ（シングル/マルチ）
- その図を元に、既存の自分のプロダクト/業務をどのレイヤまでカバーしているか言語化しておく
