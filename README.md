# Blinded Peer Reviewer (Critical, General, Blunt)

Repository scaffold for a reusable AI skill/prompt package that performs blinded scientific manuscript peer review with a validity-first, methodologically critical approach.

## Purpose

This project packages a strong peer-review instruction set for use with Codex/OpenAI- or Anthropic-style assistants. It is designed for editorial triage and substantive peer review, with emphasis on:

- scientific validity and design fit
- internal numerical consistency
- statistical adequacy (simple-first)
- overclaiming and causal overreach
- reporting completeness and reproducibility signals

## Repository Structure

- `SKILL.md` - Core skill definition and operating instructions (primary artifact)
- `agents/openai.yaml` - UI metadata for OpenAI/Codex skill catalogs
- `references/review-checklists.md` - Compact operational checklists and red flags
- `references/output-template.md` - Exact output structure template for reviews
- `examples/example-prompts.md` - Example user prompts / invocation patterns
- `CONTRIBUTING.md` - How to evolve the skill safely
- `AGENTS.md` - Repo-specific development guidance for coding agents

## Quick Start

### Use as a Codex/OpenAI skill

1. Load or copy `SKILL.md` into your skill system.
2. Optionally include `references/` files to support consistency and formatting.
3. Provide manuscript text, tables, figures, or excerpts.
4. Default mode is `FULL_METHODS + CONSISTENCY_AUDIT` unless a review mode is specified.

### Use as a system prompt (Anthropic/OpenAI)

1. Use the contents of `SKILL.md` body (or the full file minus frontmatter) as a system instruction.
2. Add manuscript content in user messages.
3. If only partial manuscript material is provided, the model should state scope limitations and avoid unsupported claims.

## Design Goals

- Blunt but professional review tone
- Evidence-linked criticism
- Decision-oriented output for editors
- Clear separation of fatal flaws vs fixable revisions
- Low hallucination risk through explicit guardrails

## Suggested Next Additions

- Discipline-specific variants (clinical, ML, epidemiology, qualitative)
- Structured JSON output mode for editor pipelines
- A manuscript consistency audit helper script (optional)
- Test fixtures with example manuscript excerpts and expected review patterns

