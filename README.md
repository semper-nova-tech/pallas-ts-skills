# Pallas TS Skills

Portable agent instructions, skills, preferences, and orchestration tooling for my
TypeScript, Angular, Hapi, and Drizzle projects.

Repository: https://github.com/semper-nova-tech/pallas-ts-skills

## Ecosystem

```text
Herdr
  terminal workspaces, tabs, panes, and agent visibility
        ↓ optional execution adapter
Pallas Agent Flow
  requirements → technical specs → Ponytail review → parallel builds → recovery
        ↓ launches
Cursor CLI agents
  implementation and repair in isolated Git worktrees
        ↓ read
Agent Lore
  AGENTS.md, Cursor rules, skills, and project preferences
```

### Agent Lore

This repository is the shared instruction layer:

- `AGENTS.md` — durable project guidance and personal preferences.
- `.cursor/rules/` — file-scoped conventions for functional TypeScript, naming,
  Angular, Hapi, Drizzle, module design, and Ponytail.
- `.agents/skills/` — reusable task workflows, including the Impeccable skills,
  LangChain/LangGraph skills, and the canonical [Ponytail skill suite](https://github.com/DietrichGebert/ponytail).

Install these files inside each target repository so they are part of that
repository's Cursor context and versioned with its code.

### Pallas Agent Flow

[Pallas Agent Flow](https://github.com/semper-nova-tech/pallas-agent-flow) is the orchestration
plugin. Its `cursor.simple` workflow uses:

1. Opus for requirements, technical-spec packets, orchestration, Ponytail review,
   recovery, and final reporting.
2. Cursor models for repository discovery and implementation.
3. One human approval gate after the Ponytail-reviewed technical specs.
4. Parallel implementation packets in isolated Git worktrees.
5. Targeted repair instead of restarting successful work.

Pallas Agent Flow is installed globally at `$PALLAS_AGENT_FLOW_HOME` or
`$HOME/tools/pallas-agent-flow`, and linked into Cursor at
`~/.cursor/plugins/local/pallas-agent-flow`.

### Cursor CLI

The Cursor Agent CLI is the implementation runtime. Pallas Agent Flow gives each
builder a bounded packet, allowed scope, guidance manifest, acceptance checks, and
worktree. Builders implement, test, report their guidance usage, and remain
available for Ponytail review or repair.

### Herdr

[Herdr](https://herdr.dev) is the terminal multiplexer and visibility layer. With
the optional Pallas Agent Flow Herdr adapter, each implementation packet gets a real
Cursor CLI child pane in a Herdr `agents` tab. Herdr shows working, blocked, and
completed agents; Pallas Agent Flow remains responsible for requirements, artifacts,
Git worktrees, reviews, and recovery.

Native Cursor delegation remains available when the Herdr adapter is not selected.

## Install

From this repository:

```bash
./install.sh /path/to/target-repo
```

The default installation adds repository-local lore and installs Pallas Agent Flow.
It will not overwrite an existing `AGENTS.md` unless explicitly forced:

```bash
./install.sh --force /path/to/target-repo
```

Skip the global Pallas Agent Flow installation when needed:

```bash
./install.sh --without-pallas-agent-flow /path/to/target-repo
```

Review installed skills and remove anything that does not fit the target project.

### Personal mode

Use `--personal` in a shared repository where the lore should stay yours alone:

```bash
./install.sh --personal /path/to/team-repo
```

- `AGENTS.md` is not installed, so the team's file is untouched.
- Skills are copied to `~/.claude/skills/`, making them user-scoped in Claude Code
  across every project.
- Cursor rules and skills are copied into the target's `.cursor/rules/` and
  `.agents/skills/`, and each copied path is added to the clone's
  `.git/info/exclude` so it never shows up in `git status`.
- `.pallas-agent-flow/` and `product/` run folders are added to `.git/info/exclude`.
- Existing files are skipped rather than replaced; `--force` replaces them.

Install Pallas Agent Flow for Claude Code at user scope rather than project scope, so
the shared `.claude/settings.json` is not modified:

```bash
claude plugin marketplace add semper-nova-tech/pallas-agent-flow
claude plugin install pallas-agent-flow@pallas-agent-flow --scope user
```

## Typical run

1. Open the target repository as one Herdr workspace.
2. Start Pallas Agent Flow with `cursor.simple`.
3. Select the `herdr` execution adapter when pane-level child visibility is wanted.
4. Let Opus create and Ponytail-review technical specs.
5. Approve the spec set once.
6. Let Cursor CLI builders implement independent packets in parallel.
7. Review and repair rejected units with Ponytail.
8. Use the persisted Pallas Agent Flow artifacts for recovery and final reporting.

Example request:

> Run Pallas Agent Flow with `cursor.simple` and the `herdr` execution adapter for this
> PRD against `main`.

## Repository contents

- `AGENTS.md` — shared instructions and preferences.
- `.agents/skills/` — reusable skills.
- `.cursor/rules/` — portable Cursor rules.
- `packages/pallas-agent-flow/` — pinned Pallas Agent Flow installation metadata.
- `source/` — preserved Cursus-specific source guidance and provenance.

This is intentionally a plain Git repository with no runtime dependency.
