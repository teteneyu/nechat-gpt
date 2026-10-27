# ねちゃっとGPT

AIにねちゃっと喋ってほしい人のためのSkillsです。
Codex、Claude Code、Claude（Web／Desktop）に導入できます。

<img src="assets/moneti.png" alt="ねちゃっとGPTのイメージ" width="640">

ネチャ度は0〜100。指定しなければ100です。
語尾や間に加えて、卑屈さや得意げな小言の濃さも変わります。
明示的に呼び出すと有効になり、そのチャットで「終了」と伝えるまで続きます。

## Claude Codeに導入する

### プラグインとして導入

ターミナルで、配布元を追加してインストールします。

```sh
claude plugin marketplace add teteneyu/nechat-gpt
claude plugin install nechat-gpt@teteneyu-nechat
```

導入後、Claude Codeで次のように呼び出してください。
一覧に出なければセッションを再起動してください。

```text
/nechat-gpt:nechat-gpt 1+1は？
```

### スキル単体で導入

このリポジトリの `plugins/nechat-gpt/skills/nechat-gpt` フォルダを、
`~/.claude/skills/nechat-gpt` にコピーしてください。
Windowsでは通常 `%USERPROFILE%\.claude\skills\nechat-gpt` です。
特定のプロジェクトだけで使う場合は、そのプロジェクトの `.claude/skills/nechat-gpt` に配置します。
すでに同名のスキルがある場合は、内容を確認してから更新してください。

単体で導入した場合は、プラグイン名の接頭辞を付けずに呼び出します。

```text
/nechat-gpt ネチャ度30で、今日の作業順を考えて。
```

プラグインと単体スキルは同じ内容なので、どちらか一方を選んでください。
Claude Codeでは `disable-model-invocation: true` により、自動での呼び出しを無効にしています。

## Claude（Web／Desktop）に導入する

1. このリポジトリをダウンロードし、`plugins/nechat-gpt/skills/nechat-gpt` フォルダをZIPにします。
2. Claudeの設定で「コード実行とファイル作成」（画面によっては「ファイルの作成と編集」）を有効にします。
3. 「カスタマイズ → スキル」（Customize > Skills）の「＋」からスキルの作成・アップロードを選び、ZIPをアップロードして有効にします。
4. チャットで「nechat-gptスキルを使って、ネチャ度30で今日の作業順を考えて」のように、スキル名を明示して依頼します。

ZIPの中は次の構造にしてください。リポジトリ全体のZIPはアップロードしません。

```text
nechat-gpt.zip
└── nechat-gpt/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

WindowsのPowerShellでは、リポジトリのルートから次のコマンドでも作成できます。
ZIPがすでにある場合は、別のファイル名を指定してください。

```powershell
Compress-Archive -LiteralPath .\plugins\nechat-gpt\skills\nechat-gpt -DestinationPath .\nechat-gpt.zip
```

Web／Desktopでは、Claude Codeの `/nechat-gpt` コマンドは使いません。
明示的に指定した場合だけ適用する条件は、スキル本文にも記載しています。
スキルのアップロード項目がない場合は、組織の設定や管理者から付与された権限も確認してください。

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

## Codexで使う

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
Claudeでも同じ言葉で終了できます。ネチャ度を指定しなければ100です。

## 内容

- `plugins/nechat-gpt/skills/nechat-gpt/SKILL.md`：会話スタイルの指示
- `plugins/nechat-gpt/skills/nechat-gpt/agents/openai.yaml`：Codexの表示名と、明示指定でのみ起動する設定
- `plugins/nechat-gpt/plugin.json`：Codex向けプラグイン情報
- `.agents/plugins/marketplace.json`：Codex向け配布元の一覧情報
- `plugins/nechat-gpt/.claude-plugin/plugin.json`：Claude Code向けプラグイン情報
- `.claude-plugin/marketplace.json`：Claude Code向け配布元の一覧情報

両方のプラグインが同じ `SKILL.md` を使います。
Claude Code用の明示呼び出し設定は `SKILL.md` の `disable-model-invocation`、Codex用は `agents/openai.yaml` の `allow_implicit_invocation` です。
`agents/openai.yaml` はCodex向けの補助情報で、Claudeの導入時に編集する必要はありません。

実行スクリプトや外部サービス接続は含みません。
会話の出方は、使うモデルや他の指示によって変わります。

## ライセンスと確認状況

[MIT License](LICENSE) で配布しています。
著作権表示とライセンス文を残せば、商用利用・改変・再配布ができます。
スキルの形式と配布ファイルの参照先を確認しています。
Claude Code 2.1.215の `claude plugin validate --strict` で、配布元とプラグインの定義の検証を通過しています。
Web／Desktop向けZIPは、`nechat-gpt/SKILL.md` を含む構造と、アーカイブの破損がないことを確認しています。
別環境へのインストールと、新しいチャットでの動作は未検証です。

## 仕様の参考

- [OpenAI Docs：Build skills](https://learn.chatgpt.com/docs/build-skills)
- [OpenAI Docs：Package your plugin](https://developers.openai.com/plugins/build/plugins)
- [Claude Code Docs：Extend Claude with skills](https://code.claude.com/docs/en/skills)
- [Claude Code Docs：Create a marketplace](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Help Center：Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude)
