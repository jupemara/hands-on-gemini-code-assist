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

## Gemini CLI がインストールされているか確認

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

```text
docs/adk-docs/docs/get-started/ にはなんのドキュメントがありますか??
```

## ステップ 4: Gemini Code Assist で最初のエージェントを作る

それでは、Gemini Code Assist を使って最初のエージェントを作成してみましょう。

### 4-1. 挨拶エージェントの作成

Gemini Code Assist に以下のように指示します：

```bash
gemini chat
```

チャットモードで以下のように質問してみましょう：

```
シンプルな挨拶エージェントを agents/greeting_agent.py に作成してください。
ユーザーの名前を受け取って挨拶を返す関数を実装してください。
```

Gemini Code Assist が生成したコードを確認し、必要に応じて修正を依頼します。

### 4-2. エージェントの実行

生成されたエージェントを実行してみましょう。

```bash
python agents/greeting_agent.py
```

### 4-3. コードの改善を依頼

Gemini Code Assist に以下のような改善を依頼してみましょう：

```
このエージェントに、時間帯によって挨拶を変える機能を追加してください。
朝（5-11時）、昼（12-17時）、夜（18-4時）で挨拶を変えてください。
```

改善されたコードを確認し、再度実行してみます。

## ステップ 5: タスク管理エージェントを作る

次は、もう少し実用的なタスク管理エージェントを Gemini Code Assist と一緒に作ってみましょう。

### 5-1. エージェントの仕様を伝える

Gemini Code Assist に以下のように指示します：

```
agents/task_manager_agent.py というファイルを作成してください。
以下の機能を持つタスク管理エージェントを実装してください：

- タスクの追加（タイトルと説明）
- タスク一覧の表示
- タスクの完了マーク
- 未完了タスクのみの表示

クラスベースで実装し、それぞれのメソッドにドキュメントを付けてください。
```

### 5-2. ADK ドキュメントを参照させる

より高度な実装のために、ADK のドキュメントを参照するよう指示します：

```
docs/adk-docs のドキュメントを参照して、
ADK のベストプラクティスに従った実装に改善してください。
```

### 5-3. テストコードの生成

Gemini Code Assist にテストコードの生成を依頼します：

```
agents/task_manager_agent.py のユニットテストを
agents/test_task_manager_agent.py に作成してください。
pytest を使用してください。
```

生成されたテストを実行してみましょう：

```bash
pytest agents/test_task_manager_agent.py -v
```

## ステップ 6: 外部 API と連携するエージェントを作る

最後に、外部 API と連携する天気情報エージェントを作成します。

### 6-1. デモ版の作成

まずはダミーデータを返すデモ版から始めましょう。Gemini Code Assist に指示します：

```
agents/weather_agent.py を作成してください。

以下の機能を持つ天気情報エージェント（デモ版）を実装してください：
- 都市名を受け取る
- ダミーの天気情報を返す（気温、天気、湿度）
- 主要都市（東京、大阪、札幌、福岡）に対応
- 存在しない都市の場合はエラーを返す
- 天気情報を見やすくフォーマットして表示

クラスベースで実装してください。
```

### 6-2. エージェントの実行

```bash
python agents/weather_agent.py
```

### 6-3. 機能の拡張（チャレンジ）

Gemini Code Assist に以下のような拡張を依頼してみましょう：

```
このエージェントに以下の機能を追加してください：
1. 複数都市の天気を一度に取得できる機能
2. 天気によってアイコン（絵文字）を表示する機能
3. JSON 形式でデータをエクスポートする機能
```

## ステップ 7: Gemini Code Assist の便利な機能を使う

### 7-1. コードの説明を求める

既存のコードを理解したい時：

```bash
gemini explain agents/task_manager_agent.py
```

### 7-2. コードのリファクタリング

コードの改善提案を受ける：

```bash
gemini refactor agents/weather_agent.py
```

### 7-3. ドキュメントの生成

README を自動生成：

```bash
gemini generate-docs agents/
```

### 7-4. バグの修正

エラーが出た時に修正を依頼：

```bash
gemini fix agents/greeting_agent.py "ImportError: No module named 'datetime'"
```

## まとめ

このチュートリアルでは、以下のことを**Gemini Code Assist との対話を通じて**学びました：

1. **Gemini Code Assist の基本的な使い方**
   - チャットモードでの対話
   - コード生成の指示の出し方
   - 段階的な機能追加の依頼方法

2. **AI との協働開発**
   - 自然言語での要件の伝え方
   - 生成されたコードのレビューと改善依頼
   - ドキュメントを参照させる方法

3. **実用的なエージェント開発**
   - シンプルなエージェントから始める
   - 段階的に機能を追加する
   - テストコードの生成と実行

4. **Gemini Code Assist の便利機能**
   - コードの説明・リファクタリング
   - ドキュメント生成
   - バグ修正の支援

## 次のステップ

### さらに学びたい方へ

- **ADK の公式ドキュメント**（`docs/adk-docs`）を読んで、より高度な機能を学ぶ
- **実際の API と連携**するエージェントを作成する（例：天気 API、ニュース API）
- **マルチエージェントシステム**を構築する
- **エージェント間の連携**を実装する

### チャレンジ課題

Gemini Code Assist を使って、以下のエージェントを作成してみましょう：

1. **ファイル管理エージェント**
   - ファイルの検索、コピー、移動
   - ディレクトリの作成・削除

2. **データ分析エージェント**
   - CSV ファイルの読み込み
   - 基本的な統計情報の表示
   - グラフの生成

3. **チャットボットエージェント**
   - ユーザーとの対話
   - 簡単な質問応答
   - コンテキストの保持

## トラブルシューティング

### Gemini Code Assist が動かない

```bash
# gcloud を最新版に更新
gcloud components update

# 再度認証
gcloud auth login
```

### 生成されたコードにエラーがある

Gemini Code Assist に具体的なエラーメッセージを伝えて修正を依頼しましょう：

```bash
gemini fix agents/your_agent.py "エラーメッセージをここに貼り付け"
```

## リソース

- [ADK Documentation](https://github.com/google/adk-docs)
- [Gemini Code Assist Documentation](https://cloud.google.com/gemini/docs/codeassist)
- [Cloud Shell Tutorials](https://cloud.google.com/shell/docs/cloud-shell-tutorials)
- [Python 公式ドキュメント](https://docs.python.org/ja/3/)

## フィードバック

このチュートリアルについてのご意見・ご感想をお待ちしています！

---

**Enjoy coding with Gemini Code Assist!** 🚀
