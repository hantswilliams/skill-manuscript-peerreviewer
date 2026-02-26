# AGENTS.md

## Project Goal

Maintain a reusable Claude Code skill for blinded scientific manuscript peer review with emphasis on methodological rigor, consistency auditing, and direct editorial usefulness.

## Editing Priorities

1. `SKILL.md` is the source of truth for all review behavior and output formatting.
2. Checklists are inlined in `SKILL.md` — do not create separate reference files.
3. Avoid provider-specific wording in the core review logic.
4. Keep `examples/example-prompts.md` updated when review behavior or output format changes.

## Style for Changes

- Prefer concise, imperative instructions.
- Preserve exact required output section numbering unless intentionally versioning.
- Do not add praise-heavy language to reviewer voice guidance.
- Treat missing manuscript details as "not reported" / "unclear".
- When adding new review modes, include expected input, workflow, and output format.
