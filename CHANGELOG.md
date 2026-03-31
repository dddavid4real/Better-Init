## [1.2.0] - 2026-03-31
### Features
- Added an optional "Claude reply efficient mode" that inserts the approved instruction block into generated `CLAUDE.md` only when the user explicitly opts in.
- Embedded the verbatim block directly in `better-init/SKILL.md` so the installed skill remains self-contained.
- Updated `README.md` to document the new option, default-off behavior, downstream naming expectations, and source acknowledgement.

### Design Rationale
- Keep Better Init's default behavior unchanged while allowing users to opt into a stricter response style.
- Embed the block in the skill so installation still works when only the `better-init` folder is copied into `~/.claude/skills/`.
- Use a user-facing mode name in skill behavior instead of leaking a temporary source-file name.
- Preserve the exact provided wording of the optional block instead of rewriting it.

### Notes & Caveats
- "Claude reply efficient mode" is included only on explicit opt-in.
- Downstream generated instructions do not mention temporary source-file names.
- The temporary source file remains in this repo only as source material for the embedded block.
