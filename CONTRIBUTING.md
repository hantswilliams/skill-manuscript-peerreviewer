# Contributing

## Scope

This repository maintains a reusable Claude Code skill for blinded manuscript peer review. Changes should improve validity-focused reviewing behavior, reduce ambiguity, or improve portability.

## Contribution Rules

- Preserve the validity-first priority hierarchy.
- Do not weaken hallucination guardrails.
- Keep the review output structure stable unless there is a strong reason to change it.
- Prefer concise, high-signal instructions over verbose prose.
- Keep checklists inlined in `SKILL.md` — do not create separate reference files.

## Updating the Skill

When changing `SKILL.md`, verify:

- Trigger description still matches intended use cases
- Review workflow order remains explicit
- Severity classification and output format are still required
- Optional modes remain consistent with default behavior
- Language remains impersonal and direct
- `metadata.version` is incremented appropriately

## Review Expectations for PRs

- State what behavior changed.
- Include at least one example prompt that benefits from the change.
- Note any compatibility impact for existing users of the skill.
- Update `examples/example-prompts.md` if output format or review behavior changed.
