# HarDoc

![HarDoc comic banner](assets/hardoc-hero.png)

> **HarDoc! Your harness is dumb right now. Fix it now!**

## Read HarDoc in your language

Each link below opens a maintained README page in that language. The commands and skill names stay in their original form so they can be copied safely.

|  |  |  |
| --- | --- | --- |
| [العربية](README.ar.md) | [বাংলা](README.bn.md) | [简体中文](README.zh-CN.md) |
| [繁體中文](README.zh-TW.md) | [Nederlands](README.nl.md) | [Français](README.fr.md) |
| [Deutsch](README.de.md) | [Ελληνικά](README.el.md) | [हिन्दी](README.hi.md) |
| [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [日本語](README.ja.md) |
| [한국어](README.ko.md) | [Bahasa Melayu](README.ms.md) | [فارسی](README.fa.md) |
| [Polski](README.pl.md) | [Português](README.pt.md) | [Română](README.ro.md) |
| [Русский](README.ru.md) | [Español](README.es.md) | [Svenska](README.sv.md) |
| [ไทย](README.th.md) | [Türkçe](README.tr.md) | [Українська](README.uk.md) |
| [Tiếng Việt](README.vi.md) | [Kiswahili](README.sw.md) | [اردو](README.ur.md) |

If your language is not listed, use [Google Translate website translation](https://translate.google.com/) and paste `https://github.com/qjc-office/hardoc`. To contribute a reviewed page, copy `README.md` to `README.<locale>.md`, translate the prose, preserve every fenced command, and add the link here.

HarDoc is a read-only harness checkup for **Claude Code and Codex**. It helps you find the instructions and tools that make an AI assistant choose the wrong skill, see the same tool twice, or spend time loading things it does not need.

## The 30-second explanation

Think of an AI coding setup as a toolbox:

- A **skill** is a recipe that tells the assistant how to do a kind of work.
- An **MCP server** is a bridge to an external tool or data source.
- A **plugin** is a bundle of skills and other components.
- A **hook** is an automatic action that runs at a lifecycle event.
- A **rule** or **agent** adds standing instructions or a specialist role.

More items do not automatically make the assistant smarter. Similar descriptions can compete, instructions can disagree, and an item that is always exposed can add noise to every request. HarDoc collects evidence before suggesting the smallest safe cleanup.

## When HarDoc is useful

Run it when:

- the assistant keeps picking the wrong skill;
- two skills appear to do the same job;
- a new plugin or MCP server made sessions slower or noisier;
- a rule, hook, or agent seems to contradict another one;
- you want to remove something but need evidence that it is safe;
- you changed the harness and need to check real work for regressions.

## Safety promise

HarDoc reports first. It does **not** delete, disable, install, edit harness configuration, auto-fix doctor findings, or send messages. A finding such as “cleanup candidate” is a proposal for a person to review, not an automatic change.

## Install for Claude Code

Run these commands once:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

Start a new Claude Code session and run:

```text
/skill-governor audit .
```

The command name stays `skill-governor` for compatibility. The plugin is branded **HarDoc**.

## Use with Codex

Codex can use the same `skill-governor` skill. If your Codex setup already exposes the skill, run:

```text
$skill-governor audit .
```

For a local installation, clone this repository and place or link `plugin/skills/skill-governor` in the skills directory used by your Codex installation:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
```

Then start a new Codex session and run `$skill-governor audit .`. The skill checks the installed Codex version and uses the native `codex doctor` surface when it is available.

## What `audit` checks

HarDoc first verifies the target directory. It then checks the runtime version and supported help output before trying the matching doctor command:

| Runtime | Doctor check | Other evidence |
| --- | --- | --- |
| Claude Code | `claude doctor` | skills, MCP, plugins, hooks, rules, agents |
| Codex | `codex doctor` | skills, MCP, plugins, hooks, rules, agents |

The report keeps these questions separate:

1. Is the item installed?
2. Is it enabled and exposed to the session?
3. Was it actually selected or invoked?
4. Is there a dependency or safety reason to keep it?
5. Did a real task still pass after a proposed change?

HarDoc does not treat a successful doctor run as proof that every task will be accurate. A doctor result is health evidence; the work itself still needs a regression check.

## Three modes

| Mode | What it means | When to use it |
| --- | --- | --- |
| `audit` | Collect read-only evidence and classify findings | Start here |
| `propose` | Turn evidence into a minimal change proposal with recovery steps | After an audit finds a real candidate |
| `evaluate` | Compare a baseline and a candidate on the same real tasks | Before claiming an improvement |

The evaluation uses the same host, model, permissions, and task prompts for both variants. It records wrong selections, missed required skills, instruction conflicts, and task outcomes separately. Token count or latency alone is not an accuracy result.

## How to read the report

- **Keep**: evidence says the component is still needed.
- **Cleanup candidate**: there is a plausible simplification, but a person should review dependencies and recovery.
- **Fix candidate**: the component appears broken or causes a reproducible problem.
- **Insufficient observation**: the data is not enough to decide.

Doctor states are also explicit:

- `COMPLETED` means the command completed; it does not mean the harness is healthy.
- `UNSUPPORTED`, `ERROR`, `TIMEOUT`, and `NOT_RUN` mean that doctor verification is `UNVERIFIED`.

If a path is missing or is a file instead of a directory, HarDoc reports an error and does not silently scan a parent or home directory.

## A beginner-friendly first run

1. Open the project you want to inspect.
2. Install HarDoc for Claude Code or expose the skill to Codex.
3. Start a fresh session so the skill list is loaded again.
4. Run `/skill-governor audit .` in Claude Code or `$skill-governor audit .` in Codex, then wait for the report.
5. Read the doctor status first.
6. Review cleanup candidates and their evidence.
7. Only then create a proposal and evaluate it against real work.

Do not delete an item only because its observed call count is zero. It may be required rarely, available only on another machine, or loaded directly by a project file.

## Compatibility notes

- The plugin machine name is `hardoc`.
- The marketplace name is `hardoc-marketplace`.
- The command slug is `skill-governor` for compatibility with earlier installations.
- Claude Code and Codex are checked independently. A result from one runtime is not copied to the other.
- If a CLI version does not support a doctor command or output option, HarDoc records that fact instead of guessing.

## License

See the repository metadata for the current license and distribution terms.
