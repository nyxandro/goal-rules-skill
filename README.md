<div align="center">

# Goal Rules

**A Claude Code skill for `/goal` mode, so your AI agent finishes a long task while you're away without stopping or overstepping.**

[![Release](https://img.shields.io/github/v/release/nyxandro/goal-rules-skill)](https://github.com/nyxandro/goal-rules-skill/releases)
[![License](https://img.shields.io/github/license/nyxandro/goal-rules-skill)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-SKILL.md-6f42c1)](https://agentskills.io/specification)
[![Claude Code plugin](https://img.shields.io/badge/Claude%20Code-plugin-d97757)](#install)

**English** · [Русский](README.ru.md)

</div>

Goal Rules is a skill for autonomous runs in Claude Code, Codex, OpenCode, Cursor and other agents
that read Agent Skills. It turns on with a `/goal` task, or whenever you hand over a task and
leave, in any wording. "Do it all to the end, don't ask me anything, I'll check when I'm back."

## Why

Two things go wrong when nobody is there to answer.

- The agent stops at the first unclear point with a question nobody will answer, and the whole
  window of time is gone.
- Or it decides everything, including what you would never allow. A push to the release branch, a
  migration on a live database, a file deleted outside the task.

These rules sit between the two. Every open point becomes a recorded decision, and a short list of
actions stays off limits however convenient it looks.

## Install

| Agent | Command |
|---|---|
| Claude Code, as a plugin | `/plugin install goal-rules --marketplace nyxandro/skills` |
| Claude Code, Codex, OpenCode, Cursor and others | `npx skills add nyxandro/goal-rules-skill` |
| Any agent, by hand | Download the [latest `.skill` archive](https://github.com/nyxandro/goal-rules-skill/releases/latest/download/goal-rules.skill) and unpack it into the agent's skills folder |

Pick one. If you install it two ways, Claude Code loads the skill twice.

<details>
<summary>More install options</summary>

<br>

- The one-line plugin install needs Claude Code 2.1.275 or later. On an older version, add the
  catalog first with `/plugin marketplace add nyxandro/skills` and then run
  `/plugin install goal-rules@nyxandro`.
- The catalog pins no version, so every commit here reaches plugin users as an update. Run
  `claude plugin marketplace update nyxandro` and `claude plugin update goal-rules@nyxandro`, or
  turn on auto-update under `/plugin` → Marketplaces.
- With `npx skills`, add `-g` to install the skill for every project. To install a given version,
  add its tag, as in `nyxandro/goal-rules-skill@v1.0.0`.
- You can also clone this repository and link the `goal-rules/` folder into your agent's skills
  folder. The skill is a single `SKILL.md`, with no scripts and no build step.

</details>

## Usage

Set the task with `/goal` and walk away. Plain words work too.

- *I'm setting a long task and leaving the computer. Don't ask me anything.*
- *Just go and do everything to the end.*
- *If something is unclear, decide it yourself and write it down.*
- *Work on your own, I'll check when I'm back.*
- *Run this overnight.*

## How it works

1. The agent starts at once. No restating the task for confirmation, no plan for approval, no
   "shall I proceed".
2. Every question becomes a decision it makes itself or a blocker it writes down. It settles an
   open point from the task text, then the project's docs, then the conventions in the code, and
   last the most conservative option that is easy to undo. Each decision is recorded with the
   options it saw and the reason.
3. It never crosses the stop-list on its own. Only the task text can allow an item, explicitly and
   by name.
4. It uses short, simple terminal commands. Long compound one-liners are what permission
   classifiers block, and nobody is around to approve them. A blocked command gets rewritten
   simpler, never worked around.
5. It works on its own branch, commits after each significant step, runs the project's checks in
   proportion to the change, finishes everything that isn't blocked and doesn't widen the scope.
6. It writes the report as it goes, from the first step, so a compacted context or a dead session
   loses nothing.

## The stop-list

| Never on its own | Allowed by default |
|---|---|
| Pushing to release or protected branches, any deployment | Commits to its own working branch |
| Force-push, rewriting shared history, deleting branches it didn't create | Local test and lint runs |
| Migrations or writes on live databases, destructive data operations | Edits inside the task scope |
| Changing configuration, secrets or files on servers | Reading anything read-only |
| Deleting or rewriting files outside the task | |
| Cancelling or re-running CI jobs | |
| Pull requests, issues, messages to people, publishing anything | |
| Spending money on services, accounts, plans or API keys | |

## Example

The final report from a made-up run, shortened.

```text
Outcome. Done partially. The CSV export works, emailing it is blocked.

Done
  a1b2c3d  Export endpoint and button, 14 tests pass
  d4e5f6a  Large exports run in the background, 3 tests pass

Decisions taken on my own
  Date format is ISO 8601, because the existing JSON export already uses it.

Blockers
  Emailing the file needs SMTP credentials. Add SMTP_URL and say "send it".

Check this first
  Admin, then Orders, then Export CSV on any date range.

Next step
  Turn on emailing once SMTP is set.
```

When you're back and ask what happened, the agent answers in five to seven lines from the report.
The next step is yours.

## Versions

The current version sits in `metadata.version` of `goal-rules/SKILL.md`, so any installed copy
tells you which one it is. Every version has a git tag and a
[release](https://github.com/nyxandro/goal-rules-skill/releases) with its own archive.
[CHANGELOG.md](CHANGELOG.md) lists what changed.

<details>
<summary>Repository layout</summary>

<br>

```text
goal-rules/SKILL.md       the skill
dist/goal-rules.skill     the skill folder as a downloadable archive
CHANGELOG.md              what changed in each version
README.md, README.ru.md   this page in English and in Russian
```

</details>

## License

[MIT](LICENSE)
