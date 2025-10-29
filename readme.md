# hands-on-gemini-code-assist

[![Open in Cloud Shell](https://gstatic.com/cloudssh/images/open-btn.svg)](https://shell.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://github.com/jupemara/hands-on-gemini-code-assist.git&cloudshell_git_branch=tutorial&cloudshell_open_in_editor=readme.md&cloudshell_tutorial=tutorial.md&cloudshell_workspace=.&ephemeral=true)

Gemini Code Assist ( Gemini CLI ) を Cloud Shell 上で使って, ADK エージェントを対話的に開発するハンズオンです.

## プロンプトサンプルたち

```
@docs/adk-docs/docs/get-started/ にはなんのドキュメントがありますか??
```

```
シンプルな挨拶エージェントを agents/greeting/agent.py に作成してください
ユーザーの名前を受け取って挨拶を返す関数を実装してください
- gemini 2.5 flash を使います
- `adk run` コマンドを使って実行
- `adk web --port 8080` コマンドを使って開発者が動作確認を行います
```

```
時間帯によって挨拶を変える機能を追加します
以下の時間帯で挨拶を変えてください

- 朝 ( 5-11時 )
- 昼 ( 12-17時 )
- 夜 ( 18-4時 ) 
```