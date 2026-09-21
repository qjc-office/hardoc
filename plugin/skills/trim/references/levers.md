# Levers: what can be turned down, and how

Verify every key against the installed runtime version before using it. Keys and accepted values change between releases, and a stale CLI earlier on `PATH` may not know a key that the running build supports. Read the version from the binary that actually executes, not from whatever `which` resolves.

## Files this skill may edit

| File | Holds |
| --- | --- |
| `~/.claude/settings.json` | Skill overrides, plugin enablement, hooks, memory excludes |
| `~/.claude.json` | MCP servers at user scope, per-project MCP approvals |
| `~/.codex/config.toml` | Codex skills, MCP servers, plugins, feature flags |
| `~/.codex/hooks.json` | Codex hooks |
| `~/.claude/agents/`, or a project's `.claude/agents/` | Agent definitions written by a person. Touched only under `--include-hooks`, and only by moving a file to `~/.claude/hardoc/disabled-agents/`, never by deleting or editing it. Generated agent files are excluded here as everywhere else: change their source instead |

Project-scoped equivalents (`.claude/settings.json`, `.mcp.json`) follow the same rules when the person asks for a project-level change.

The runtime writes to these same settings files while it is running. Read each file immediately before writing it, merge into what is actually there, and write once. Never build an edit from a copy read minutes earlier, or a setting the person changed in between disappears. Where a CLI command exists for the change, prefer it over editing the file, because it handles this and keeps derived state consistent.

## Files this skill must not edit

| File | Why |
| --- | --- |
| Installed-plugin inventory under the plugins directory | Generated from `enabledPlugins`. Editing it desynchronizes state |
| Marketplace registry | Owned by the `plugin marketplace` CLI |
| Managed or policy settings | Cannot be excluded or overridden, and must not be worked around |
| Plugin caches, generated agent files | Not the source. Change the source and let the existing sync produce them |

## Reversible levers (preferred)

| Target | Edit | Undo |
| --- | --- | --- |
| Skill from a skills directory (Claude Code) | `skillOverrides: { "<name>": "name-only" \| "user-invocable-only" \| "off" }` | Remove the key |
| Skill provided by a plugin (Claude Code) | **No per-skill lever exists.** The override above is not consulted for these skills and does nothing. The only lever is disabling the whole plugin | Re-enable the plugin |
| All bundled skills (Claude Code) | `disableBundledSkills: true`. Blunt: it removes every shipped skill and workflow at once. Offer it only when the person says they never use them | Remove the key |
| Plugin (Claude Code) | `enabledPlugins: { "<plugin>@<marketplace>": false }`. Write `false`; do not delete the key | Set `true` |
| Plugin (Claude Code, via CLI) | `claude plugin disable <plugin>` | `claude plugin enable <plugin>` |
| MCP from a project manifest | Add the server name to the project's `disabledMcpjsonServers` list | Remove it from the list |
| Rule loaded on every session | Add a glob for it to `claudeMdExcludes` | Remove the glob |
| Rule loaded on every session (alternative) | Add `paths:` frontmatter so it loads only for matching work | Remove the frontmatter key |
| Skill, MCP server or plugin (Codex) | `enabled = false` in the matching `config.toml` section | Delete that line |
| MCP server inside a Codex plugin | `enabled = false` on the nested server section, leaving siblings alone | Delete that line |

Prefer the CLI when one exists. `plugin disable` and `mcp remove` keep derived state consistent; hand-editing the same value does not.

## Destructive levers (opt-in only)

| Target | Why it is destructive | Requirement |
| --- | --- | --- |
| A single hook | No supported disable flag exists. Hook entries accept only their type, command, timeout and async fields. The entry has to be cut out of the settings file | Snapshot, plus `--include-hooks` |
| A single agent | No supported disable flag exists in agent frontmatter or settings. The file has to be moved out of the agents directory, to `~/.claude/hardoc/disabled-agents/`, so undo is a move back | Snapshot, plus `--include-hooks` |

Two notes on hooks. Commenting a hook command out is not a supported disable path and must not be proposed. And a global switch that disables every hook usually disables the status line with it, so it is not a substitute for turning off one noisy hook.

## Estimating standing cost

| Target | Measure |
| --- | --- |
| Skill | Length of the description exposed in the skill listing |
| Rule | Bytes of files that load unconditionally, meaning no `paths:` frontmatter |
| MCP server | Size of the tool schemas exposed to the session. When deferred loading or tool search is active, do not count every installed schema as injected |
| Plugin | Sum of the skills, MCP servers and hooks it contributes |
| Hook | Registration count and, where observable, execution time |

Report cost as an estimate with the measure named. Do not convert it into a claim about task accuracy.
