# **STEP 1 - Lesson 1: LivebookをセットアップしてHello Worldを出力する**

## **🎯 ゴール**
- Elixir 開発環境（Livebook）をセットアップする
- Elixir の基本的なコードを書き、Hello World を出力する
- Elixir の REPL (IEx) の使い方を学ぶ
- **「プログラミングの第一歩は簡単！」** と感じてもらう

---

## **⏳ 1時間のスケジュール**
| 時間 | 内容 |
|------|------|
| **0:00 - 0:10** | **イントロダクション**（この講座の学び方・心構え） |
| **0:10 - 0:20** | **環境構築 & Livebook のセットアップ** |
| **0:20 - 0:30** | **Elixir の基本構文 & Hello World** |
| **0:30 - 0:50** | **ワーク: 自分で Elixir のコードを書いてみる** |
| **0:50 - 1:00** | **振り返り & 質疑応答** |

---

## **1. イントロダクション（0:00 - 0:10）**
### **💡 伝えること**
- **この講座の学習方針（ミルフィーユ型学習）**
  - **「1つずつ完璧にしない！」**
  - **「全体の流れを先に学び、徐々に深掘りしていく」**
- **Elixir を学ぶとどんなことができるのか？**
  - Webアプリ開発（Phoenix Framework）
  - 分散システム（Erlang VM）
  - 機械学習（Nx, Axon）
- **本日のゴール**
  - **Elixir の開発環境（Livebook）をセットアップし、Hello World を出力する**
  - **まずはプログラムを書いて実行することを楽しむ！**

---

## **2. 環境構築 & Livebook のセットアップ（0:10 - 0:20）**
### **🔹 必要なツールの紹介**
- **エディタ: [Visual Studio Code](https://code.visualstudio.com/)**
- **コード管理: [GitHub](https://github.com)**
- **対話型環境（Jupyter Notebook 的なもの）: [Livebook](https://livebook.dev/)**

### **🔹 Livebook のインストール & 起動**
1. [Livebookの公式サイト](https://livebook.dev/) にアクセス
2. 「Install Livebook」からインストール手順を確認
3. `livebook server` を実行し、ブラウザで開く

💡 **環境構築でつまずいたらすぐに質問！**

---

## **3. Elixir の基本構文 & Hello World（0:20 - 0:30）**
### **🔹 Elixir の特徴**
- 関数型言語
- 並行処理が簡単
- Erlang VM（BEAM）上で動作
- シンプルな構文

### **🔹 Hello World を出力**
💡 **最初のコードを書いてみる！**
```elixir
IO.puts "Hello, World!"