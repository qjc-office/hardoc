# HarDoc

![HarDoc コミックバナー](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc は Claude Code と Codex のハーネスを読み取り専用で点検します。重複または衝突する指示を見つけ、アシスタントが誤った skill を選ぶ原因を確認します。

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Claude Code にインストール

次の2つのコマンドを一度だけ実行します。

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Codex へのローカルインストール

Codex に skill を直接インストールするには、リポジトリをクローンしてローカルの skills フォルダーにリンクを作成します。

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
```

## Claude Code で使う

新しい Claude Code セッションを開き、次を実行します。

```text
/skill-governor audit .
```

## Codex で使う

Codex に skill が表示されている場合は、新しいセッションで次を実行します。

```text
$skill-governor audit .
```

## HarDoc が確認する内容

HarDoc は対象ディレクトリを確認し、CLI バージョンを調べてから各ランタイムの native doctor を試します。

- `claude doctor`: Claude Code のインストール状態を確認します。
- `codex doctor`: Codex のインストール状態を確認します。
- `audit`: skills、MCP、plugins、rules、hooks、agents と実際の使用証拠を確認します。

## 安全範囲

HarDoc は読み取り専用です。ハーネス設定の削除・無効化・インストール・変更を行わず、doctor の結果も自動修正しません。変更前に提案を確認してください。

詳しい説明と評価手順は [English README](README.md) を参照してください。
