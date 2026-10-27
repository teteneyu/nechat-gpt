# ねちゃっとGPT

AIにねちゃっと喋ってほしい人のためのSkillsです。

<img src="assets/moneti.png" alt="ねちゃっとGPTのイメージ" width="640">

ネチャ度は0〜100。指定しなければ100です。
語尾や間に加えて、卑屈さや得意げな小言の濃さも変わります。
明示的に呼び出すと有効になり、そのチャットで「終了」と伝えるまで続きます。

## Codexに導入する

このリポジトリは、スキルを1つ含むプラグインとして構成しています。
配布元は [teteneyu/nechat-gpt](https://github.com/teteneyu/nechat-gpt) です。

### プラグインとして導入

Codex CLIが使える環境で、配布元を追加します。

```sh
codex plugin marketplace add teteneyu/nechat-gpt
```

デスクトップアプリを再起動し、プラグイン一覧の配布元から「ねちゃっとGPT」を選んでインストールしてください。
配布元の名前は `teteneyu-nechat` です。
GitHubへの公開だけでは、OpenAIの公開プラグインディレクトリには掲載されません。

### スキル単体で導入

Codexに次のように依頼する方法もあります。

```text
$skill-installer で https://github.com/teteneyu/nechat-gpt/tree/main/plugins/nechat-gpt/skills/nechat-gpt をインストールして。
```

手動で入れる場合は、このリポジトリの `plugins/nechat-gpt/skills/nechat-gpt` フォルダを、
自分の `~/.agents/skills/nechat-gpt` にコピーしてください。
Windowsでは通常 `%USERPROFILE%\.agents\skills\nechat-gpt` です。
すでに同名のスキルがある場合は、内容を確認してから更新してください。
導入後に一覧へ出なければCodexを再起動してください。

プラグインと単体スキルは同じ内容なので、導入方法はどちらか一方を選んでください。

## 使う

Codexで `$` を入力し、一覧から `nechat-gpt` を選んで質問します。
プラグインから導入した場合は、配下の同名スキルを選んでください。

```text
$nechat-gpt 1+1は？
```

粘度を控えめにするなら、数字を添えます。

```text
$nechat-gpt ネチャ度30で、今日の作業順を考えて。
```

普通の話し方へ戻したいときは、そのチャットで「ねちゃっとGPTを終了」と伝えてください。

## 内容

- `plugins/nechat-gpt/skills/nechat-gpt/SKILL.md`：会話スタイルの指示
- `plugins/nechat-gpt/skills/nechat-gpt/agents/openai.yaml`：表示名と、明示指定でのみ起動する設定
- `plugins/nechat-gpt/plugin.json`：プラグイン情報
- `.agents/plugins/marketplace.json`：配布元の一覧情報

実行スクリプトや外部サービス接続は含みません。
会話の出方は、使うモデルや他の指示によって変わります。

## ライセンスと確認状況

[MIT License](LICENSE) で配布しています。
著作権表示とライセンス文を残せば、商用利用・改変・再配布ができます。
スキルの形式と配布ファイルの参照先を確認しています。
別環境へのインストールと、新しいチャットでの動作は未検証です。

## 仕様の参考

- [OpenAI Docs：Build skills](https://learn.chatgpt.com/docs/build-skills)
- [OpenAI Docs：Package your plugin](https://developers.openai.com/plugins/build/plugins)
