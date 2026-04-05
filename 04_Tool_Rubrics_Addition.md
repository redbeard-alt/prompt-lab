# 04_TOOL ADDITIONS: EVALUATION RUBRICS
# Append this section to the existing 04_Tool_Quick_Reference_Card_v2.md
# Also: REMOVE the following sections from 04_Tool since they now live elsewhere:
#   - 6-Part Formula table (lives in 01_Core Part 2)
#   - Outcomes-Based Prompting section (lives in 02_Core Part 3)
#   - Keep ONLY the lookup tables, phrases, and cheat sheets in 04_Tool

---

## EVALUATION RUBRICS

Use these when running Perfection Loop / Monte Carlo testing.
Pick the rubric that matches your output type. Score each dimension 1-10.

### Rubric A: Writing & Documents

| Dimension | 10 = | 1 = |
|-----------|------|-----|
| **Accuracy** | All claims verifiable, no hallucinations | Contains fabricated facts |
| **Completeness** | Covers all requested elements, no gaps | Missing major sections |
| **Clarity** | Every sentence unambiguous, logical flow | Confusing, contradictory |
| **Format Compliance** | Matches spec exactly | Ignores format instructions |
| **Actionability** | Reader knows exactly what to do next | Vague, no next steps |
| **Tone Match** | Nails requested voice | Wrong register entirely |

### Rubric B: Research & Analysis

| Dimension | 10 = | 1 = |
|-----------|------|-----|
| **Source Quality** | Peer-reviewed, primary sources, recent | Unverified, outdated, blog-only |
| **Depth** | Surfaces non-obvious insights, cross-references | Surface-level summary |
| **Balance** | Represents multiple perspectives fairly | One-sided or biased |
| **Data Integrity** | Statistics cited with sources, methodology noted | Numbers without attribution |
| **Synthesis** | Connects dots across sources into new insight | Just lists findings |
| **Practical Value** | Clear implications and recommendations | Academic without application |

### Rubric C: Code & Technical

| Dimension | 10 = | 1 = |
|-----------|------|-----|
| **Correctness** | Runs without errors, produces expected output | Broken, wrong results |
| **Efficiency** | Optimal approach for the problem size | Unnecessarily complex or slow |
| **Readability** | Clear naming, logical structure, minimal comments needed | Opaque, tangled |
| **Edge Cases** | Handles nulls, empty inputs, boundaries | Crashes on unexpected input |
| **Security** | No injection vectors, input validation | Vulnerable to basic attacks |
| **Maintainability** | Easy to modify, extend, or debug | Brittle, tightly coupled |

### How to Use in Prompts

Append to any prompt that needs quality gating:

```
Before finalizing, score your output against this rubric:
[paste relevant rubric dimensions]
If any dimension scores below 7, revise that aspect before showing me the result.
```

---

## Scope Note

These rubrics are for evaluating prompts, model outputs, and workflows. Shell commands, Docker invocations, and OS-level procedures must live in Terminal Lab, with DRY-RUN and risk labels, and only be referenced here at a high level.
