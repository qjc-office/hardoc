# HarDoc

![HarDoc 漫畫橫幅](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc 是適用於 Claude Code 與 Codex 的唯讀 harness 檢查工具。它會找出重複或衝突的指示，避免助理選錯 skill。

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## 在 Claude Code 中安裝

只需執行以下兩個指令一次：

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## 在 Claude Code 中使用

開啟新的 Claude Code 工作階段，然後執行：

```text
/skill-governor audit .
```

## 在 Codex 中使用

如果 Codex 已顯示此 skill，請開啟新工作階段並執行：

```text
$skill-governor audit .
```

## HarDoc 會檢查什麼

HarDoc 先驗證專案目錄，再檢查 CLI 版本，並嘗試執行對應執行環境的原生 doctor。

- `claude doctor`: 檢查 Claude Code 安裝健康狀況。
- `codex doctor`: 檢查 Codex 安裝健康狀況。
- `audit`: 檢查 skills、MCP、plugins、rules、hooks、agents 與實際呼叫證據。

## 安全界線

HarDoc 只讀執行。它不會刪除、停用、安裝或修改 harness 設定，也不會自動修復 doctor 結果。請先人工審閱建議。

完整說明與評估流程請查看 [English README](README.md)。
