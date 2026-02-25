# AGENTS.md

## Project Goal

Maintain a reusable skill/prompt package for blinded scientific manuscript peer review with emphasis on methodological rigor, consistency auditing, and direct editorial usefulness.

## Editing Priorities

1. `SKILL.md` is the source of truth.
2. Keep `agents/openai.yaml` consistent with `SKILL.md`.
3. Put long checklists/templates in `references/` instead of bloating `SKILL.md`.
4. Avoid provider-specific wording in the core review logic.

## Style for Changes

- Prefer concise, imperative instructions.
- Preserve exact required output section numbering unless intentionally versioning.
- Do not add praise-heavy language to reviewer voice guidance.
- Treat missing manuscript details as "not reported" / "unclear".

