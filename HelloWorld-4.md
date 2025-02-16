# Elixir で学ぶ簡単なシステム開発

## 1. 環境構築
- Elixir のインストール（asdf や Homebrew）
- IEx（対話型シェル）を使った基本的なコマンド実行
- LiveBook をセットアップし、対話的にコードを実行

## 2. 基本構文の学習
- データ型（整数、リスト、マップ、タプル）
- パターンマッチング
- 関数の定義と再帰
- 高階関数（Enum, Stream）
- パイプ演算子（|>）を使ったデータフロー処理

## 3. 並行処理の基礎
- Elixir のプロセス（spawn, send, receive）
- Agent, Task を使った並列処理
- GenServer による状態管理

## 4. Web API 開発（Phoenix Framework）
- `mix phx.new` でプロジェクト作成
- ルーティング（Router）
- コントローラーとビューの作成
- Ecto によるデータベース操作
- WebSocket / LiveView を活用したリアルタイム更新

## 5. LiveBook を使った機械学習
- Nx を使った数値計算
- Axon を使ったニューラルネットワークの学習
- データ可視化（VegaLite）

## 6. 分散システムの基礎
- Node を起動してリモートプロセス間通信
- 分散タスクを Supervisor で管理
- OTP の基本概念（GenServer, Supervisor, ETS）

## 7. クラウドデプロイ
- Fly.io や Gigalixir にデプロイ
- Docker コンテナを作成し、コンテナ環境で実行