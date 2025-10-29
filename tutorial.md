# Gemini Code Assist で始める AI エージェント開発ハンズオン

## 概要

このチュートリアルでは, Google Cloud Shell 上で **Gemini Code Assist (Gemini CLI)** を使用して, Agent Development Kit (ADK) によるエージェントを**対話的に開発する体験**をします.

Gemini Code Assist に指示を出しながら, 実際にコードを生成/改善していく過程を学びます.

## ここで学べそうなこと

- Gemini Code Assist の使い方
- Gemini との対話でコードを生成する方法
- ドキュメントを参照させながら開発する方法

## Google アカウント認証

Google Account の確認です

```bash
gcloud auth list
```

認証済みアカウントが正しくコンフィグに設定されているか確認します

```bash
gcloud config get-value account
```

もし

```
Credentialed Accounts

ACTIVE: *
ACCOUNT: hogehoge@example.com
```

のようにログイン済みのアカウントがうまく出ていない場合は,

```bash
gcloud auth application-default login --no-launch-browser
```

を実行してログインを行います (ログイン URL が出てくるので, URL をクリック, verification code を入力しましょう)

## Gemini CLI の起動

Cloud Shell Editor の terminal ペインを出現させます.
画面左上の `terminal` ボタンをクリックしてください ( File Edit Selection View Go Run **Terminal** Help と並んでいます ) 

`gemini` コマンドが使えることを確認します

```bash
gemini --version
```

Gemini CLI を立ち上げておきます (以降のエージェントのやり取りは, ここか Cloud Shell Editor の右側の Gemini ペインから行います)

```bash
gemini
```

## ADK ドキュメントをセットアップする

コーディングエージェントに ADK の公式ドキュメントを読ませるために手元に最新版のドキュメントをダウンロードします.

```bash
git submodule update --init --recursive
```

この段階でドキュメントの内容を Gemini Code Assist に読み込ませることもできます

```
@docs/adk-docs/docs/get-started/ にはなんのドキュメントがありますか??
```

## ADK 環境構築

Python の仮想環境を作成して, ADK をインストールします

### ADK のインストール

```bash
pip install google-adk
```

## Gemini Code Assist で最初のエージェントを作る

Gemini Code Assist を使って最初のエージェントを作成してみましょう

### 挨拶エージェントの作成

```
シンプルな挨拶エージェントを agents/greeting/agent.py に作成してください
ユーザーの名前を受け取って挨拶を返す関数を実装してください
- gemini 2.5 flash を使います
- `adk run` コマンドを使って実行
- `adk web --port 8080` コマンドを使って開発者が動作確認を行います
```

### エージェントの実行

生成されたエージェントを実行してみましょう。

```bash
adk run agents/greeting/agent.py
```

### コードの改善

Gemini Code Assist に以下のような改善を依頼してみましょう：

```
時間帯によって挨拶を変える機能を追加します
以下の時間帯で挨拶を変えてください

- 朝 ( 5-11時 )
- 昼 ( 12-17時 )
- 夜 ( 18-4時 ) 
```

### localhost:8080 にて動作確認

```bash
cd agents && adk web --port 8080
```

## タスク管理エージェントを作る

お次は, もう少し実用的なタスク管理エージェントを Gemini Code Assist と一緒に作ってみましょう

```
/clear
```

このコマンドで先程までのタスクのコンテキストをリセットしておきましょう

### まずはエージェントの仕様を考える

まずはエージェントと仕様に詰めてみましょう

```
agents/task_manager/readme.md にタスク管理エージェントの仕様をファイル作成します

## 機能

- タスクの追加
- タスク一覧の表示
- 完了したタスクの完了マーク
- 未完了タスクのみ表示するか完了タスクのみ表示するかユーザが決められる
- 完了タスクに関しては完了日時を記録する

## AI モデル

- gemini-2.5-flash を利用
```

### 仕様に基づいてエージェントを実装させる

```
@agents/task_manager/readme.md にタスクマネージャーエージェントの仕様を記載しました

agents/task_manager/agent.py に仕様に記載したタスク管理エージェントを実装してください
```

適宜コードを修正したり, Gemini と会話してタスク管理エージェントを完成させてください

```bash
cd agents && adk web --reload --port 8080
```

### リファクタリングやベストプラクティスの適用

より高度な実装のために, ADK のドキュメントを参照するよう指示します
( GEMINI.md にも一応記載してあるのですが,明示的に指定してみます. このタスクは AI の期限によっては失敗する可能性があります... )

```
@docs/adk-docs のドキュメントを参照して,
ADK のベストプラクティスに従った実装にリファクタリングしてみてください
```

### テストコードの生成 (チャレンジ問題)

Gemini Code Assist にテストコードの生成を依頼します：

```
@agents/task_manager/agent.py のユニットテストを @agents/task_manager/test_agent.py に作成します

- pytest を使用します
- テストのお作法は t_wada の TDD 従ってください
```

生成されたテストを AI に実行させて, エラーや失敗がないか, あれば適宜修正してもらいましょう

```
`pytest agents/test_task_manager_agent.py -v`
を実行して, テストが失敗したら修正してください
```

## refs

- [ADK Documentation](https://google.github.io/adk-docs/)
- [Gemini Code Assist Documentation](https://github.com/google-gemini/gemini-cli/blob/main/docs/get-started/index.md)
