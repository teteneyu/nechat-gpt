# ねちゃっとGPT

AIにねちゃっと喋ってほしい人のためのスキルです。
Codex・Claude Code・Claude（Web／Desktop）で使えます。

<img src="assets/moneti.png" alt="ねちゃっとGPTのイメージ" width="640">

ネチャ度は0〜100。指定しなければ100です。
呼び出したチャットで有効になり、「ねちゃっとGPTを終了」で普通の話し方に戻ります。

## 導入

### Claude Code

```sh
claude plugin marketplace add teteneyu/nechat-gpt
claude plugin install nechat-gpt@teteneyu-nechat
```

### Codex

```sh
codex plugin marketplace add teteneyu/nechat-gpt
```

アプリを再起動し、プラグイン一覧の配布元 `teteneyu-nechat` からインストールしてください。

### Claude（Web／Desktop）

[スキルフォルダ](plugins/nechat-gpt/skills/nechat-gpt)をフォルダごとZIPにして、「カスタマイズ → スキル」からアップロードしてください。

## 使い方

Codexでは `$nechat-gpt`、Claude Codeでは `/nechat-gpt:nechat-gpt` を付けて話しかけます。
ClaudeのWeb／Desktopでは「nechat-gptスキルを使って」と伝えてください。

```text
$nechat-gpt ネチャ度30で、今日の作業順を考えて。
```

詳しい指示は [SKILL.md](plugins/nechat-gpt/skills/nechat-gpt/SKILL.md) にあります。
会話の出方はモデルによって変わります。

[MIT License](LICENSE)
