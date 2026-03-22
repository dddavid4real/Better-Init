# Better Init for Claude Code

A Claude Code skill for bootstrapping a new project folder with the right long-lived context.

Instead of stuffing everything into `CLAUDE.md`, **Better Init** helps Claude create:
- a concise, project-specific `CLAUDE.md`
- a small set of durable reference docs under `doc/` by default
- an approval-first setup flow that drafts before writing files

## What the skill does

Better Init guides Claude to:
- identify the real target directory instead of assuming the whole workspace is one project
- inspect local files before inventing commands, tooling, or architecture
- ask only for missing essentials
- keep `CLAUDE.md` concise and path-based
- store richer project context in focused markdown files
- adapt the setup for coding, research, or mixed workspaces
- separate durable reference docs from optional planning files
- show the proposed structure and `CLAUDE.md` draft before writing anything

## When to use it

Use this skill when you want Claude to:
- initialize a new project folder
- create or refresh a project `CLAUDE.md`
- set up reusable project context for future sessions
- organize project background into markdown files instead of one giant instruction file
- bootstrap a research project, coding repo, or mixed workspace without bad defaults

Typical examples:
- a fresh code repository that still needs project-local instructions
- a research folder with papers, notes, datasets, and scripts
- a mixed workspace where Claude should not invent repo-wide commands
- any project where you want a draft-first, confirm-before-write setup

## Key behaviors

Better Init is opinionated in a few important ways:
- **Minimal intake**: reuse what the user already said and ask only for missing essentials
- **User preferences preserved**: include the user's preferred name and core working rules in the drafted `CLAUDE.md`
- **`doc/` by default**: use `doc/` for durable references unless the user wants another folder
- **Concise `CLAUDE.md`**: keep it focused on durable instructions and file references
- **Planning support only when useful**: use planning files for non-trivial setups, not for every bootstrap
- **Draft first**: never write files before showing the proposed structure and asking for approval

## Prerequisite

Before using Better Init, install the `planning-with-files` skill:

- Repo: https://github.com/OthmanAdi/planning-with-files

Better Init is designed to work with it for non-trivial project initialization flows.

## Installation

Copy the `better-init` folder into your personal Claude skills directory:

```bash
git clone https://github.com/dddavid4real/Better-Init.git
cd Better-Init
cp -R better-init ~/.claude/skills/
```

After copying, start a new Claude Code session or reload your current one so the skill list refreshes.

## Usage

Invoke the skill directly:

```text
/better-init
```

Or provide a little context up front:

```text
/better-init initialize this research folder
```

```text
/better-init set up this new repo with a clean CLAUDE.md
```

```text
/better-init this folder has papers, scripts, and notes; draft the structure first
```

## What a successful run should produce

A good Better Init run usually ends with:
- a concise `CLAUDE.md`
- a small, useful set of reference docs under `doc/`
- project instructions that match the real folder contents
- no invented commands or boilerplate
- clear confirmation before any files are written

## Expected project structure

After using Better Init, a project will usually end up with something like this:

```text
your-project/
├── CLAUDE.md
├── task_plan.md
├── findings.md
├── progress.md
└── doc/
    ├── background.md
    ├── architecture.md
    ├── dataset.md
    └── workflow.md
```

The exact files depend on the project.

For example:
- coding projects may lean toward `architecture.md`, `domain-boundaries.md`, or `verification.md`
- research projects may lean toward `background.md`, `dataset.md`, `experiments.md`, or `literature.md`
- mixed workspaces may use a smaller hybrid set

The planning files come from `planning-with-files`:
- `task_plan.md`
- `findings.md`
- `progress.md`

The important idea is simple:
- `CLAUDE.md` stays short and operational
- detailed, durable context lives in separate markdown files
- planning files track non-trivial setup work across sessions
- Claude gets clearer project guidance with less clutter

## Acknowledgement
Part of the idea is from @Tw93: https://x.com/HiTw93/status/2032091246588518683

## License

MIT. See [LICENSE](./LICENSE).
