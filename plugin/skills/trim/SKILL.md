---
name: trim
description: "Reduce the harness exposure a person does not need. Builds a short role profile, ranks skills, plugins, MCP servers, rules, hooks and agents by always-on cost, previews the change set, and applies it only after approval with a one-command rollback. Triggers: trim my harness, too many skills, reduce context, declutter, turn off unused skills or MCP servers, my assistant keeps picking the wrong skill. Not for: read-only diagnosis (use skill-governor audit), installing anything, or editing project source."
---

# Trim

HarDoc has two surfaces. `skill-governor` collects evidence and stops. `trim` turns that evidence into a change a person approved, and keeps a way back.

The goal is not a smaller item count. It is a harness where the assistant sees what this person actually works on.

## Usage

- Claude Code: `/trim`, `/trim --dry-run`, `/trim restore <snapshot-id>`
- Codex: `$trim`

| Flag | Effect |
| --- | --- |
| `--dry-run` | Preview only. Write nothing at all, including the stored profile. |
| `--reprofile` | Ask the profile questions again and overwrite the stored answers. Combined with `--dry-run`, ask them but store nothing. |
| `--include-hooks` | Allow hook and agent candidates, which require destructive edits. Off by default. |
| `--level off` | Raise the default prescription from `name-only` to `off` for role-unrelated items. |
| `restore <id>` | Roll a snapshot back. |

## The core move: lower exposure instead of deleting

Claude Code's `skillOverrides` setting takes four values per skill name. Verify them against the installed version before relying on them.

| Value | Effect | Use for |
| --- | --- | --- |
| `on` (absent) | Name and description both exposed | Keep |
| `name-only` | Name listed, description withheld | **Default prescription for a skill from a skills directory.** The skill still works; only its standing token cost drops |
| `user-invocable-only` | Hidden from the model, `/name` still works | Rarely needed, but should not be auto-selected |
| `off` | Hidden from both | Confirmed unused |

Start at `name-only`. A wrong guess there costs nothing: the capability survives and a person can still invoke it. Reserve `off` for items the person names, or for `--level off` runs.

### In Claude Code, this lever does not reach plugin-provided skills

In Claude Code a per-skill override applies to skills loaded from a skills directory. For a skill that came from a plugin the setting is not consulted at all: the skill stays fully listed no matter what the override says. Writing one for a plugin skill is a silent no-op, and reporting a saving from it is a false success.

So classify every candidate by source before prescribing anything.

| Source | Available lever, or prescribing rule, in Claude Code |
| --- | --- |
| A skills directory (user, project, or a link into one) | The four levels above, per skill |
| A plugin | Only the plugin as a whole, through `enabledPlugins`. There is no per-skill lever |
| Bundled with the runtime | Only all of them at once, through `disableBundledSkills` |
| Anything else, or a source that could not be resolved | No prescription. Report it as `unknown` and leave it alone |

When a plugin's skills are the expensive part, the honest proposal is "disable this plugin" with its full cost, not a per-skill override that will do nothing. If the person wants to keep part of a plugin, say that the runtime does not support it.

HarDoc ships as a plugin, so this limit covers `skill-governor` and `trim` themselves.

Confirm the behavior against the installed version rather than assuming it, and treat "the override is ignored for plugin skills" as the default assumption until a version proves otherwise.

**This particular limit is a Claude Code observation, and it should not be carried over to Codex unchecked.** Codex keys its per-skill setting by path, and it can address an MCP server nested inside a plugin, which suggests its addressing model may differ here. Whether that extends to a plugin's skills is unverified, and the nested-server observation is not evidence that it does. Check the installed Codex configuration before either prescribing such a change or refusing one, and say which of the two runtimes an observation came from.

Until that check is done on a Codex run, prescribe nothing there for a skill whose source you could not resolve. A skipped candidate costs a little standing context; a confidently wrong prescription costs trust in every other row of the table.

The same preference for reversible form applies elsewhere. Plugins are disabled by writing `false`, not by deleting the key. Rules can be demoted from always-loaded to path-scoped instead of being removed.

## Steps

### 1. Profile

Ask at most four questions, then stop asking. Read `references/profile.md` for the question set and the matching rules. Store answers in `~/.claude/hardoc/profile.json` and reuse them on later runs unless `--reprofile` is given. Under `--dry-run`, keep the answers in memory for that run and write nothing, so the flag's promise holds literally.

A profile is a hypothesis about what this person does, not a fact about what they need. It ranks candidates; it never decides alone.

### 2. Inventory and cost

Reuse the collection contract in the `skill-governor` skill (its `references/harness-audit.md`, §2). Do not write a second inventory implementation. For every item add four fields:

- `source`: where the item is loaded from. This decides which lever exists at all, so resolve it before anything else and leave it `unknown` rather than guessing. An item whose source is unknown gets no prescription.
- `always_cost`: what this item injects into every session regardless of the request. Skill description length, bytes of a rule file with no `paths:` frontmatter, exposed MCP tool schemas, registered hook count.
- `role_match`: `related`, `unclear`, or `unrelated` against the profile.
- `recent_use`: whether any observed evidence shows recent use. Absence of evidence is `unknown`, never zero.

Rank candidates by `always_cost` descending within `role_match = unrelated`. An item with a large standing cost and no relation to the person's work is the best candidate. A cheap item is rarely worth touching even when unused.

### 3. Preview

Read [references/levers.md](references/levers.md) before proposing anything. It fixes which files may be edited, which must never be touched, the reversible form for each target, and how standing cost is measured.

Print one table: item, current state, proposed level, estimated saving, evidence, and how to undo it. Put the total saving on top. Name every item that was considered and kept, with the reason.

Write nothing in this step. A person must be able to run the preview on a whim.

### 4. Apply

1. Snapshot first. Copy every file about to change into `~/.claude/hardoc/snapshots/<timestamp>/` and write `manifest.json` recording each item's previous value. For a change that moves a file rather than editing one, record both paths, and keep the moved file outside the snapshot directory, under `~/.claude/hardoc/disabled-agents/<timestamp>/<scope>/`. A snapshot is a backup a person may delete once the change looks settled, and the only copy of their agent must not disappear with it. Never move onto an occupied path; report the collision instead.
2. Apply the approved subset only. If the person approved part of the list, do not apply the rest.
3. Re-parse every edited file. If a JSON or TOML file no longer parses, restore the snapshot immediately and report the failure.
4. Confirm the change took effect by re-observing what the runtime exposes. A file that parses is not a change that applied. A lever the runtime ignores leaves a perfectly valid file behind, which is exactly what a silent no-op looks like, so a parse check cannot tell the two apart. Report anything that did not take effect as failed, and do not count its saving.
5. Print the rollback command: `/trim restore <timestamp>`.

`restore` compares the current value against the manifest. When a value changed after the snapshot, report the conflict and leave it alone rather than overwriting somebody's later edit.

## Safety

- **Hooks and agents are opt-in.** Neither has a supported disable flag, so turning one off means cutting an entry out of a settings file or moving a file. They stay out of the applied set unless `--include-hooks` is given, and they always require a snapshot.
- **Zero observed calls is not a reason to remove anything.** This rule is inherited from `skill-governor` and is not relaxed here. An item may be exposed only on another machine, invoked directly by a project file, or needed rarely.
- **Dependencies win over counts.** Language servers, security hooks and verification hooks stay even at zero skill invocations.
- **Recent use is a veto.** Any item with recent-use evidence leaves the candidate list regardless of role match.
- **Never write derived files.** Plugin state belongs in the settings `enabledPlugins` map; the installed-plugins inventory is generated from it. Marketplace registration belongs to the CLI.
- **Read the version from the binary that actually runs.** A stale CLI shim elsewhere on PATH may predate the settings keys this skill relies on. Confirm the schema against the running version before proposing a key it may not support.
- Never install, update, log in, or change a managed policy file to make a change succeed.

## Reporting

Report in this order: what changed, what was kept and why, anything that was attempted and did not take effect, the total saving from confirmed changes only, snapshot id, rollback command.

Count a saving only for a change that step 4 confirmed. An unsupported lever produces no saving no matter how clean the edit looked.

State savings as estimates. Standing token cost is measurable; task accuracy is not measured by this skill. When a person asks whether the harness got better, hand them back to `skill-governor evaluate`, which compares real tasks. A smaller context is not by itself an improvement.
