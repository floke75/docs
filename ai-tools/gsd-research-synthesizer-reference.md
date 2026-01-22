# gsd-research-synthesizer.md — Summary Reference

## Metadata
| Attribute | Value |
|-----------|-------|
| **Type** | Agent |
| **Location** | `agents/gsd-research-synthesizer.md` |
| **Size** | 247 lines |
| **Documentation Tier** | Summary |
| **Complexity Score** | 1+2+2+1 = **6/12** |

### Complexity Breakdown
- **Centrality: 1** — Single spawn point (new-project), single consumer (roadmapper)
- **Complexity: 2** — 8-step execution flow, synthesis across 4 files, confidence assessment
- **Failure Impact: 2** — Poor synthesis = poorly informed roadmap = cascading planning issues
- **Novelty: 1** — Aggregation/synthesis patterns are standard

---

## Purpose

Synthesizes research outputs from 4 parallel researcher agents into a cohesive SUMMARY.md that informs roadmap creation. Spawned after STACK, FEATURES, ARCHITECTURE, and PITFALLS research completes. The key distinction: **Synthesized, not concatenated**—findings are integrated with clear recommendations, not just copied together.

---

## Critical Behaviors

- **Be opinionated** — Roadmapper needs clear recommendations, not wishy-washy summaries
- **Synthesize, don't concatenate** — Integrate findings across files, identify patterns
- **Include roadmap implications** — Suggest phase structure with rationale
- **Assess confidence honestly** — Reflect actual source quality from research files
- **Commit ALL research files** — Researchers write but don't commit; synthesizer commits everything

---

## Execution Flow

| Step | Action | Output |
|------|--------|--------|
| 1 | Read all 4 research files | Parsed findings |
| 2 | Synthesize executive summary | 2-3 paragraph overview |
| 3 | Extract key findings | Summaries from each file |
| 4 | Derive roadmap implications | Phase suggestions with rationale |
| 5 | Assess confidence | Levels per area + gaps |
| 6 | Write SUMMARY.md | Using template `~/.claude/get-shit-done/templates/research-project/SUMMARY.md` |
| 7 | Commit all research | Single commit with all 5 files |
| 8 | Return summary | Structured confirmation |

---

## Inputs (4 Research Files)

| File | Extract |
|------|---------|
| `STACK.md` | Recommended technologies, versions, rationale |
| `FEATURES.md` | Table stakes, differentiators, anti-features |
| `ARCHITECTURE.md` | Patterns, component boundaries, data flow |
| `PITFALLS.md` | Critical/moderate/minor pitfalls, phase warnings |

---

## Interactions

| Reads | Writes | Spawned By | Consumed By |
|-------|--------|------------|-------------|
| `.planning/research/STACK.md` | `.planning/research/SUMMARY.md` | `/gsd:new-project` | `gsd-roadmapper` |
| `.planning/research/FEATURES.md` | git commit (all 5 files) | | |
| `.planning/research/ARCHITECTURE.md` | | | |
| `.planning/research/PITFALLS.md` | | | |

---

## SUMMARY.md Sections

How roadmapper uses each section:

| Section | How Roadmapper Uses It |
|---------|------------------------|
| **Executive Summary** | Quick understanding of domain |
| **Key Findings** | Technology and feature decisions |
| **Implications for Roadmap** | Phase structure suggestions |
| **Research Flags** | Which phases need deeper research |
| **Confidence Assessment** | Trustworthiness of each research area |
| **Gaps to Address** | What to flag for validation |
| **Sources** | Basis for confidence and follow-up verification |

---

## Roadmap Implications Format

For each suggested phase, include:

- **Rationale** — Why this order based on research
- **What it delivers** — Key outcomes
- **Features from FEATURES.md** — Which features belong here
- **Pitfalls to avoid** — From PITFALLS.md warnings

Add research flags:
- Which phases need `/gsd:research-phase` during planning
- Which phases have well-documented patterns (skip research)

---

## Confidence Assessment

| Area | Confidence | Notes |
|------|------------|-------|
| Stack | HIGH/MEDIUM/LOW | Source quality from STACK.md |
| Features | HIGH/MEDIUM/LOW | Source quality from FEATURES.md |
| Architecture | HIGH/MEDIUM/LOW | Source quality from ARCHITECTURE.md |
| Pitfalls | HIGH/MEDIUM/LOW | Source quality from PITFALLS.md |

---

## Structured Returns

**SYNTHESIS COMPLETE:**
```markdown
## SYNTHESIS COMPLETE

**Files synthesized:**
- .planning/research/STACK.md
- .planning/research/FEATURES.md
- .planning/research/ARCHITECTURE.md
- .planning/research/PITFALLS.md

**Output:** .planning/research/SUMMARY.md

### Executive Summary
[2-3 sentence distillation]

### Roadmap Implications
Suggested phases: [N]
1. **[Phase name]** — [one-liner rationale]
2. **[Phase name]** — [one-liner rationale]
3. **[Phase name]** — [one-liner rationale]

### Research Flags
Needs research: Phase [X], Phase [Y]
Standard patterns: Phase [Z]

### Confidence
Overall: [HIGH/MEDIUM/LOW]
Gaps: [list any gaps]

### Ready for Requirements
SUMMARY.md committed. Orchestrator can proceed to requirements definition.
```

**SYNTHESIS BLOCKED:**
```markdown
## SYNTHESIS BLOCKED

**Blocked by:** [issue]
**Missing files:** [list any missing]
**Awaiting:** [what's needed]
```

---

## Quality Indicators

- **Synthesized, not concatenated** — Findings are integrated, not just copied
- **Opinionated** — Clear recommendations emerge from combined research
- **Actionable** — Roadmapper can structure phases based on implications
- **Honest** — Confidence levels reflect actual source quality

---

## Quick Reference

```
WHAT:     Synthesize 4 research files into SUMMARY.md for roadmapper
MODES:    Single mode (synthesis)
OUTPUT:   .planning/research/SUMMARY.md + git commit of all 5 research files

CORE RULES:
• Synthesize (integrate) not concatenate (copy)
• Be opinionated with clear recommendations
• Include phase suggestions with rationale
• Commit ALL research files (researchers don't commit)

SPAWNED BY: /gsd:new-project (after 4 researchers complete)
CONSUMED BY: gsd-roadmapper (Executive Summary, Implications, Flags)
```
