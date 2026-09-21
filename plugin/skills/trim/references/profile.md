# Profile: four questions, then stop

The profile ranks candidates. It never decides alone, and it never overrides observed use.

## Questions

Ask these once and store the answers. Offer choices rather than open text wherever possible, and let the person skip any question.

1. **Main work on this machine.** Writing code, writing documents and content, data and analysis, design, operations and management. Multiple answers allowed.
2. **Stack, if code was selected.** Languages and frameworks in daily use.
3. **Not done here.** Work the person is confident they never do on this machine. This is the strongest signal in the set, because it is a statement rather than an inference.
4. **Machine role.** Only machine, one of several, or a shared or temporary machine. A person who works across machines should see fewer aggressive proposals, because evidence collected here covers less of their work.

Store the answers as `~/.claude/hardoc/profile.json` with the timestamp and the runtime version they were collected under. A profile older than six months should be confirmed rather than trusted silently.

## Matching rules

| Signal | Classification |
| --- | --- |
| Item's domain named in question 3 | `unrelated`, highest confidence |
| Item's domain unrelated to every answer in questions 1 and 2 | `unrelated` |
| Item's domain matches an answer | `related` |
| Domain cannot be determined from the item's own metadata | `unclear` |

Classify from the item's own name, description and declared dependencies. Do not read an item's body to guess its domain unless it is already a candidate; reading everything on every run is what this skill exists to avoid.

`unclear` is not a candidate. It is reported so the person can label it, and a label they give becomes part of the profile.

## What the profile cannot do

- It cannot override recent-use evidence. Evidence wins.
- It cannot justify removing a dependency. A language server matters to someone who writes code even if they never invoke a skill from it.
- It cannot be inferred from the current working directory alone. One project is not the person's whole job.
- It cannot be filled in on the person's behalf. If they skip every question, run on standing cost alone and say in the report that role matching was skipped.

## Shared machines

When question 4 says the machine is shared or temporary, restrict proposals to `name-only`, never propose hooks or agents even with the flag, and say why in the report. One person's unused item is another person's daily tool.
