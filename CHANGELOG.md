# Changelog

The current version is `metadata.version` in `goal-rules/SKILL.md`. Every version is tagged
`vX.Y.Z` in git and published as a GitHub release with its own `.skill` archive. Versions are
numbered MAJOR.MINOR.PATCH.

- **PATCH** (1.0.1) is a fix or clearer wording. The skill behaves the same.
- **MINOR** (1.1.0) is a new or changed rule, for example an item added to the stop-list.
- **MAJOR** (2.0.0) changes how the agent works in goal mode, such as when it may stop or where
  the report goes.

## [1.1.0] - 2026-11-06

### Changed

- The description says what the skill does and when to use it, without retelling the steps of
  the work. With the steps in the description, the model can follow them and skip the body of the
  skill, as Superpowers' tests showed. The trigger phrases are unchanged.

## [1.0.0] - 2026-11-06

The first numbered version. The skill itself is unchanged since `8bef474`. This release adds the
version number to `SKILL.md`.

## Before 1.0.0

- **2026-10-24.** The skill installs as a Claude Code plugin from the
  [nyxandro/skills](https://github.com/nyxandro/skills) catalog (`8bef474`).
- **2026-09-13.** First version. How an agent works when the owner sets a `/goal` task and leaves
  (`3eb6320`).
