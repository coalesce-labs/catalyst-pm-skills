# catalyst-pm-skills

Catalyst PM skills — Linear **backlog grooming**. Cross-harness, installable with `npx skills`.

One skill today: **`groom-backlog`** — scans a Linear backlog and reports orphaned issues (no
project), misplaced issues (wrong project), stale issues (no activity > 30 days), potential
duplicates, and issues missing estimates, then offers to generate the Linear update commands.

## Install

One command, for every coding agent on the machine:

```sh
npx skills@latest add coalesce-labs/catalyst-pm-skills --all
```

It installs the skill into each agent it detects (Claude Code, Codex, Cursor, OpenCode and the
rest). Add `-g` to install into your home directory instead of the project. Skills installed this
way do not auto-update; run `npx skills update -y` to refresh them.

<details><summary><strong>One agent at a time</strong></summary>

```sh
npx skills@latest add coalesce-labs/catalyst-pm-skills -a codex
npx skills@latest add coalesce-labs/catalyst-pm-skills -a cursor
npx skills@latest add coalesce-labs/catalyst-pm-skills          # OpenCode, Amp, Windsurf, …
```

Without `--all` the installer asks which skills to take and which agents to install them on.
</details>

<details><summary><strong>Alternative for Claude Code: the plugin marketplace</strong></summary>

The plugin rail also registers the `backlog-analyzer` sub-agent (which `npx skills` cannot — it
installs SKILL.md skills only, never agents or hooks).

```
/plugin marketplace add coalesce-labs/catalyst-pm-skills
/plugin install catalyst-pm@catalyst-pm-skills
```

Pick one rail; installing both leaves you with the skill twice.
</details>

## Prerequisites

- [`linearis`](https://www.npmjs.com/package/linearis) — Linear CLI (`npm install -g linearis`)
- `gh` — GitHub CLI (optional, for PR ↔ issue cross-checks)
- `jq` — JSON processing
- A `.catalyst/config.json` (or legacy `.claude/config.json`) with your Linear team key:
  `{ "catalyst": { "linear": { "teamKey": "TEAM" } } }`

The skill works best alongside [`catalyst-dev`](https://github.com/coalesce-labs/catalyst): its
`groom-backlog` flow delegates backlog fetching to catalyst-dev's `linear-research` agent. Without
catalyst-dev installed, run the Linear fetch yourself and hand the JSON to the analysis step.

## What's inside

```
skills/groom-backlog/
  SKILL.md                     # the skill
  scripts/                     # co-located so `npx skills` copies them with the skill
    check-prerequisites.sh
    pm-utils.sh
    workflow-context.sh
  agents/
    backlog-analyzer.md        # Claude sub-agent (plugin rail only)
```

## Provenance

Extracted from the [`coalesce-labs/catalyst`](https://github.com/coalesce-labs/catalyst) monorepo
(`plugins/playground/pm-ops`) per **CTL-2306** — the effort to collapse that repo to the `dev`
plugin and move the rest to their own repos. `groom-backlog` is the one PM skill that survived the
CTL-2218 audit and the CTL-2237 triage (which removed the other 11 `catalyst-pm-ops` skills as
built on multi-person-org assumptions this solo-dev repo doesn't have). This is a clean copy with
this note, not a history-preserving split — the source path moved (CTL-1999) and the content was
heavily pruned, so a subtree split would carry little of value. See the source repo's history for
pre-extraction changes.

## License

MIT — see [LICENSE](./LICENSE).
