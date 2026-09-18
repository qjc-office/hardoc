# HarDoc

HarDoc audits Claude Code and Codex harnesses for duplicate, conflicting, or unnecessarily exposed skills, MCP servers, plugins, hooks, rules, and agents. It keeps diagnosis read-only and requires `claude doctor` or `codex doctor` plus task-level regression evidence.

## Install from Claude Code marketplace

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

Then start a new Claude Code session and invoke:

```text
/skill-governor audit .
```

The `skill-governor` slug remains stable for compatibility; the plugin is branded **HarDoc**.

## Scope

HarDoc reports evidence and minimal proposals. It never deletes, disables, installs, edits harness configuration, auto-fixes doctor findings, or sends external messages.
