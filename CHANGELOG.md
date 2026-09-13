# Changelog

## 1.0.0

Initial standalone release. Extracted `groom-backlog` (the surviving `catalyst-pm-ops` skill),
its supporting scripts, and the `backlog-analyzer` agent from
`coalesce-labs/catalyst` `plugins/playground/pm-ops` (source commit `e4212b984`) into a
cross-harness `npx skills`-installable bundle, per CTL-2306.

- Scripts co-located under `skills/groom-backlog/scripts/` so the `npx skills` copy carries them.
- Script-path resolution in `SKILL.md` now falls back to the skill-local `scripts/` dir when
  `CLAUDE_PLUGIN_ROOT` is unset (non-Claude harnesses).
- Prior in-monorepo history: `catalyst-pm-ops` v2.x/v3.0.0; CTL-2237 removed 11 of 12 skills;
  CTL-1999 moved the plugin under `plugins/playground/`.
