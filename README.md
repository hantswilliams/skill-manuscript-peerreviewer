# 🔬 Blinded Peer Reviewer — Claude Code Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Standard: Agent Skills](https://img.shields.io/badge/Standard-Agent%20Skills-green.svg)](https://github.com/anthropics/claude-code)
[![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-orange.svg)](SKILL.md)

A validity-first, methodologically critical **blinded peer review** skill for Claude Code. Designed for pre-submission and preprint evaluation of original research manuscripts.

---

## ✨ What It Does

| Capability | Description |
|:-----------|:------------|
| 🎯 **Validity-first review** | Prioritizes scientific validity and design fit over novelty or style |
| 🔢 **Consistency auditing** | Systematic cross-check of numbers across abstract, text, tables, and figures |
| 📊 **Statistical adequacy** | Simple-first statistical review — flags p-value-only conclusions, missing CIs, multiplicity |
| ⚠️ **Overclaiming detection** | Flags causal language from observational designs, overgeneralization, unsupported conclusions |
| 📋 **Reporting completeness** | Checks against CONSORT, STROBE, PRISMA, TRIPOD, and other standards |
| 📎 **Supplementary audit** | Verifies supplement consistency or flags missing supplements as a concern |
| 🔄 **Revision response audit** | Comment-by-comment verification of author responses to prior reviews |

---

## 🚀 Quick Start

### Prerequisites

- [Claude Code](https://github.com/anthropics/claude-code) installed and configured

### Installation (Global)

Clone the repo and copy the skill into your Claude Code skills directory:

```bash
git clone https://github.com/hantswilliams/skill-manuscript-peerreviewer.git
```

```bash
mkdir -p ~/.claude/skills && cp skill-manuscript-peerreviewer/SKILL.md ~/.claude/skills/blinded-peer-reviewer.md
```

### Installation (Project-Level)

To scope the skill to a single project:

```bash
mkdir -p .claude/skills
```

```bash
cp /path/to/skill-manuscript-peerreviewer/SKILL.md .claude/skills/blinded-peer-reviewer.md
```

### Download Without Cloning

If you just want the skill file:

```bash
mkdir -p ~/.claude/skills && curl -sL https://raw.githubusercontent.com/hantswilliams/skill-manuscript-peerreviewer/main/SKILL.md -o ~/.claude/skills/blinded-peer-reviewer.md
```

### Verify Installation

After installing, start Claude Code and check that the skill is loaded:

```bash
claude
```

You should see `blinded-peer-reviewer` listed among available skills. Then provide a manuscript for review:

```
Review this manuscript as a blinded peer reviewer.
[paste or attach manuscript]
```

---

## 📂 Repository Structure

```
.
├── SKILL.md                  # Core skill definition (primary artifact)
├── examples/
│   └── example-prompts.md    # Example invocations with expected output
├── AGENTS.md                 # Development guidance for coding agents
├── CONTRIBUTING.md           # Contribution rules and PR expectations
├── LICENSE                   # MIT License
└── .github/
    ├── PULL_REQUEST_TEMPLATE.md
    └── ISSUE_TEMPLATE/
        └── skill-change.md
```

---

## 🎛️ Review Modes

| Mode | Use When |
|:-----|:---------|
| `FULL_METHODS` | You want a complete methodological critique *(default)* |
| `CONSISTENCY_AUDIT` | You want a numeric/metric mismatch audit only *(default)* |
| `RAPID_SCREEN` | You need quick editorial triage — reject vs revision |
| `STATS_SIMPLE` | You want a non-specialist statistical adequacy pass |
| `CLINICAL_RELEVANCE` | You want emphasis on practical significance and applicability |
| `REVISION_RESPONSE_AUDIT` | You have a revised manuscript + prior reviewer comments |

> **Default:** `FULL_METHODS + CONSISTENCY_AUDIT` when no mode is specified.

Specify a mode at the start of your prompt:

```
Mode: RAPID_SCREEN. Triage this manuscript for likely reject vs revision.
[paste manuscript]
```

---

## 📄 Output Structure

Every review produces a structured 12-section output:

| # | Section | Purpose |
|:-:|:--------|:--------|
| 0 | Material Inventory & Review Scope | What was received, what's missing, confidence level |
| 1 | Overall Recommendation | Reject / Major Revision / Minor Revision / Accept |
| 2 | Summary Assessment | 3-6 sentence overview of claims vs evidence |
| 3 | Fatal Flaws | Rejection-level issues with validity impact |
| 4 | Major Concerns | Substantive revision required |
| 5 | Moderate Concerns | Important but not decision-critical |
| 6 | Minor Concerns | Editorial / low priority |
| 7 | Internal Consistency Audit | Cross-section numerical mismatches |
| 8 | Statistical Review | Simple-first statistical adequacy |
| 9 | Supplementary Materials Assessment | Supplement audit or absence flag |
| 10 | Claims That Overreach the Evidence | Overclaiming with phrasing suggestions |
| 11 | Priority Revisions | Top 3-7 ranked revisions for credibility |

---

## 🔍 Scope

### ✅ In Scope

- Original research articles (clinical, epidemiological, computational, translational, bench science)
- Pre-submission drafts and preprint manuscripts
- Revision responses with prior reviewer comments

### ❌ Out of Scope

- Commentaries, editorials, opinion pieces, letters
- Grant proposals
- Copyediting, reference formatting, journal-specific compliance
- Plagiarism detection

The skill will explicitly decline non-research material and explain why.

---

## 📝 Examples

See [examples/example-prompts.md](examples/example-prompts.md) for 9 detailed examples including:

- Full manuscript review with default mode
- Abstract-only review with expected output sample
- ML/prediction model manuscript review
- Revision response audit with multi-document input
- Manuscript with missing supplementary materials

---

## 🤝 Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Key rules:

- Preserve validity-first priority hierarchy
- Don't weaken hallucination guardrails
- Keep checklists inlined in `SKILL.md`
- Increment `metadata.version` when behavior changes
- Include example prompts in PRs that change review behavior

---

## 📜 License

[MIT](LICENSE)
