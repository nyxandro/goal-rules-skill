# Goal Rules Skill

[![Download Goal Rules Skill](https://img.shields.io/badge/Download-goal--rules.skill-blue?style=for-the-badge)](https://github.com/nyxandro/goal-rules-skill/raw/main/dist/goal-rules.skill)

A goal mode skill for Claude Code and OpenCode: the rules an autonomous agent works by when the
owner sets a long task and walks away. It activates on a `/goal` task and on any wording of "do
it all to the end, don't ask me anything, I'll check when I'm back".

Two things go wrong when nobody is there to answer. The agent stops on the first ambiguity with
a question that will not be answered, and the whole window of time is lost. Or the agent decides
everything, including what the owner would never have allowed: a push to the release branch, a
migration on a live database, a deleted file outside the task. These rules sit between the two.

## What the agent does

1. Starts at once. No restating the task for confirmation, no plan for approval, no "shall I
   proceed".
2. Turns every question into either a decision it makes itself or a blocker it writes down.
   Open points are resolved from the task text, then the project's docs, then the code's own
   conventions, then the most conservative reversible option. Every decision is recorded with
   the options seen and the reason.
3. Never crosses the stop-list on its own: no pushes to release branches or deployments, no
   force-push, no writes to live databases, no changes on servers, no deletions outside the
   task, no cancelled CI jobs, no pull requests, issues, messages or publications, no spending.
   Only the task text can allow one of these, explicitly and by name.
4. Uses short, simple terminal commands. Compound one-liners are what permission classifiers
   block, and nobody is around to approve them; a blocked command is rewritten simpler and
   split further until it passes, never worked around.
5. Works on its own branch, commits after each significant step, follows the project's checks
   in proportion to the change, finishes everything that is not blocked and widens nothing.
6. Writes the report as it goes, from the first step, so a compacted context or a dead session
   loses nothing. The report is appended to the document the task came in, or to the file the
   owner named; no new file is invented.

## The final report

Outcome in the first line; what was done with commits, tests and their real results; decisions
taken alone, with alternatives; blockers and exactly what permission unblocks each; what was not
done and why; the user-visible signal to check first; one proposed next step. When the owner is
back and asks what happened, the answer is five to seven lines from the report, and the next
step is theirs.

## Install

**Claude Code, as a plugin**, from [nyxandro/skills](https://github.com/nyxandro/skills), the
catalog of my skills:

```text
/plugin install goal-rules --marketplace nyxandro/skills
```

Use one way or the other: with both, Claude Code loads the skill twice.

**Any agent, as a skill folder:**

Download `dist/goal-rules.skill` (the badge above) and unpack it into the skills folder of your
agent, or clone this repository and link the `goal-rules/` folder there. The skill is a single
`SKILL.md`; no scripts, no build step.

## Repository layout

```text
goal-rules/SKILL.md     the skill
dist/goal-rules.skill   downloadable archive of the skill folder
```

## License

MIT.
