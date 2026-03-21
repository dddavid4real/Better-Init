---
name: better-init
description: >-
  Initialize a new project folder with a concise CLAUDE.md, durable project context,
  and linked reference markdown files instead of making the user restate everything
  from scratch. Use this whenever the user wants to bootstrap a fresh directory,
  initialize project context, create or reset a project CLAUDE.md, set up a project
  contract, or start a new research/coding project with reusable instructions and
  reference docs. This skill is especially relevant when the project is new,
  underspecified, mixed-purpose, or needs file-based context organization.
metadata:
  version: "1.1.0"
  scope: personal
---

# Better Init

Bootstrap a new project directory so future sessions have the right durable context without bloating `CLAUDE.md`.

The goal is to create a clean, reusable setup:
- `CLAUDE.md` stays concise and operational
- richer project context lives in markdown files under a reference folder
- the workflow adapts to the real project type instead of copying a generic coding template

## When to use this skill

Use this skill when the user wants to:
- initialize a brand new project folder
- create, regenerate, or clean up `CLAUDE.md`
- set up project-specific context in a new directory
- start a research project, coding project, or mixed workspace and avoid repeating the same instructions later
- establish a reusable project contract plus linked background docs

## Core principles

1. **Reuse context already given.** If the user already described the project, do not ask them to repeat it.
2. **Ask only for missing essentials.** Use a minimal intake.
3. **Keep `CLAUDE.md` short.** Store details in reference docs and link to them by path.
4. **Adapt to the project.** Research projects, coding repos, and mixed folders need different contracts.
5. **Draft before writing.** Show the proposed structure and `CLAUDE.md` draft, then ask for confirmation before creating or updating files.
6. **Do not invent tooling.** Only include commands or architecture boundaries you actually discovered.

## Workflow

### 1. Identify the target project directory

First, determine the real working folder.

- If the user named a directory, use that.
- If they are already inside the intended project directory, confirm that from context.
- If the current location is a mixed workspace, do not treat the whole workspace as one project.

Before drafting anything:
- read any existing `CLAUDE.md`
- inspect the local directory structure
- inspect project-local config files before assuming build/test/lint commands

If the target directory is ambiguous, ask first.

### 2. Run minimal intake

Reuse information already present in the conversation. Only ask for what is missing.

Always gather these essentials:
1. **Project intro** — but only if the user has not already provided it
2. **Preferred name** — ask what the user wants Claude to call them
3. **Reference-doc folder** — default to `doc/`; only ask if the user wants to override it

Also ask clarifying questions when needed for:
- project type (research, coding, mixed, other)
- whether an existing `CLAUDE.md` should be replaced or merged
- any missing high-value constraints that would materially change the contract

Also ask clarifying questions first, before proposing files, when the request is ambiguous about the target directory, project type, or whether this should be a coding, research, or mixed setup.

Keep the intake short. Do not interrogate the user with unnecessary setup questions.

## Required standing instructions for the drafted `CLAUDE.md`

Include these user-level instructions in the draft:
- Always start conversation responses with the user's preferred name followed by a comma
- Always ask first when something important is unclear or uncertain
- Always figure out the clear plan before starting substantive work

Write these as concise project instructions, not as a long biography or transcript.

### 3. Optional planning support for non-trivial setups

Use planning files only as optional execution support for non-trivial setup work.

Before confirmation:
- decide whether planning support would help
- mention that choice in the draft
- explain what would go into planning files versus durable reference docs
- do not invoke `planning-with-files` yet

After confirmation:
- if the approved setup is long-running, exploratory, or multi-phase, invoke `planning-with-files` if it is available and appropriate in the current environment
- otherwise skip planning files entirely and keep the setup lean

Use planning support only for tasks such as:
- multi-step initialization that will continue after bootstrap
- research-heavy discovery work
- setup work that needs explicit progress tracking across sessions

Important distinctions:
- planning files such as `task_plan.md`, `findings.md`, and `progress.md` are execution-tracking artifacts
- reference docs under `doc/` are the durable project references future sessions should consult
- planning files should not replace durable topic docs like `doc/background.md` or `doc/architecture.md`

If you do use planning files:
- keep them in the project directory, not the skill directory
- do not paste large planning contents into `CLAUDE.md`
- reference them from `CLAUDE.md` only when they are genuinely useful to future work

### 4. Propose a reference-doc structure

Use `doc/` as the default reference folder.

Create only the files that the project actually needs. Examples:
- `doc/background.md`
- `doc/architecture.md`
- `doc/dataset.md`
- `doc/experiments.md`
- `doc/workflow.md`

Rules:
- do not create speculative or empty docs
- prefer a few meaningful files over many shallow ones
- separate durable context by topic
- keep file names obvious and stable

For research-heavy projects, favor files like:
- background
- datasets
- experiments
- literature
- workflow

For coding-heavy projects, favor files like:
- architecture
- domain-boundaries
- environment
- verification

For mixed projects, use a hybrid structure.

### 5. Draft a project-specific `CLAUDE.md`

Draft `CLAUDE.md` so it is short, operational, and easy to scan.

It should usually include:

```markdown
# Project Contract

## Project Overview
- One concise paragraph on what this project is for

## Reference Files
- `doc/background.md` — [what it contains]
- `doc/...` — [what it contains]
- `task_plan.md` / `findings.md` / `progress.md` — [if relevant]

## User Preferences
- Start responses with "<preferred-name>, "
- Ask first when something important is uncertain
- Establish a clear plan before substantive work

## Build And Test / Research Workflow / Working Approach
- Include only what is actually relevant to this project type

## Safety Rails
### NEVER
- Project-specific things to avoid

### ALWAYS
- Project-specific things to preserve or verify

## Verification
- Only real, discovered verification steps

## Compact Instructions
Preserve:
1. Architecture or research decisions that should not be re-derived
2. Modified files and key changes
3. Current verification status
4. Open risks, TODOs, and rollback notes
```

Adapt the middle sections to the actual project:

#### If this is a coding project
You may include sections like:
- Build And Test
- Architecture Boundaries
- Coding Conventions
- Verification

But only include commands or boundaries if you actually discovered them.

#### If this is a research project
Prefer sections like:
- Research Overview
- Data / Dataset References
- Experiment Tracking
- Scripts / Notebooks / Pipelines
- Validation Workflow

#### If this is a mixed project
Blend both styles, but keep it concise.

## 6. Show the draft before writing

Before creating or updating files, present:
1. the proposed reference folder and files
2. the proposed `CLAUDE.md` structure
3. the actual `CLAUDE.md` draft text
4. a brief note on what will be stored in planning files versus reference docs

Then ask for confirmation.

Do **not** write files until the user approves.

## 7. After approval, write the files

Once the user approves:
- create or update `CLAUDE.md`
- create the chosen reference folder if needed
- create only the approved reference markdown files
- write the topic-specific content into those files
- keep `CLAUDE.md` limited to concise operating instructions plus file references
- if planning support was approved and the work is genuinely non-trivial, invoke `planning-with-files` and keep those planning files separate from the durable reference docs

After writing:
- read back the files you created or updated
- verify that referenced paths actually exist
- summarize the resulting structure briefly for the user

## Anti-patterns

Avoid these mistakes:
- copying a JavaScript project contract into a non-JS project
- inventing install/dev/test/lint commands
- assuming the workspace root is the project root in a heterogeneous directory
- dumping all project background directly into `CLAUDE.md`
- creating too many markdown files up front
- skipping the confirmation step before writing files
- invoking `planning-with-files` before the user approves a non-trivial setup draft
- asking the user to restate context they already gave you

## Output expectations

When using this skill successfully, the result should be:
- a concise `CLAUDE.md`
- a small set of stable reference docs under `doc/` by default
- optional planning files only when the initialization is long-running or genuinely non-trivial
- a clear distinction between execution-tracking files and durable reference docs
- a project contract that matches the real work instead of a copied template

## Example trigger phrases

This skill should be a strong match for prompts like:
- "initialize this new project folder"
- "set up a CLAUDE.md for this research project"
- "bootstrap this directory so I don't have to repeat the context every time"
- "create a project contract and put detailed context into separate markdown files"
- "start this new repo and set up persistent project instructions"
