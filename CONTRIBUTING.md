# Contributing

## Scope

This repository maintains a reusable AI skill for blinded manuscript peer review. Changes should improve validity-focused reviewing behavior, reduce ambiguity, or improve portability across AI platforms.

## Contribution Rules

- Preserve the validity-first priority hierarchy.
- Do not weaken hallucination guardrails.
- Keep the review output structure stable unless there is a strong reason to change it.
- Prefer concise, high-signal instructions over verbose prose.
- Keep provider-specific metadata (`agents/openai.yaml`) aligned with `SKILL.md`.

## Updating the Skill

When changing `SKILL.md`, verify:

- trigger description still matches intended use cases
- review workflow order remains explicit
- severity classification and output format are still required
- optional modes remain consistent with default behavior
- language remains impersonal and direct

## Review Expectations for PRs

- State what behavior changed.
- Include at least one example prompt that benefits from the change.
- Note any compatibility impact for existing users of the skill.

