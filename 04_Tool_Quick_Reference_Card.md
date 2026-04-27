# PROMPT LAB: QUICK REFERENCE CARD
> ALL lookup tables, cheat sheets, and decision shortcuts in one place.
> For templates → 03_Tool | For frameworks → 01_Core | For debugging → 06_Troubleshooting
> Last updated: April 2026

---

## CUSTOM INSTRUCTIONS PHILOSOPHY

- Keep global custom instructions short and high-leverage (3–7 bullets on tone, structure, and proactivity).
- Do not paste multi-page rule sets into the permanent box; they narrow the model and reduce flexibility.
- Control verbosity per prompt instead: e.g., "Give me the bottom line in 100 words or less" or "Aim for a concise 3–5 paragraph explanation."

---

## MODEL SELECTION

| Scenario | Recommended Model |
|----------|------------------|
| Quick factual lookup | Lightweight chat (Pro) |
| Complex analysis, multi-step reasoning | Reasoning model (Claude Opus, ChatGPT 5.2) |
| Creative writing, brainstorming | Chat model with high temperature |
| Code generation / debugging | Claude Opus or ChatGPT 5.2 |
| Multi-model deliverable | Perplexity Computer (auto-routes) |

**Rule of thumb:** Use reasoning models when the task is complex (many steps, high stakes, deep analysis), even if the format is "simple" (e.g., an important email). Use lighter chat models for quick answers and low-stakes drafts.

---

## ROUTER NUDGE PHRASES

Append one to any complex or high-stakes prompt to push the model into deeper reasoning:

| Phrase | When to Use |
|--------|-------------|
| Think hard about this. | Default for complex tasks |
| Think deeply about this. | Deep analysis, nuanced topics |
| Think carefully about this. | High-stakes, precision-critical |

> **WARNING:** For dedicated reasoning models, avoid "think step by step" by default. They already reason internally; over-constraining can hurt performance. Prefer a clear TASK plus constraints.

---

## VERBOSITY CONTROL PHRASES

Append one to every prompt to control output length:

| Phrase | Approximate Length |
|--------|--------------------|
| Give me the bottom line in 100 words or less. Use markdown. | Ultra-short |
| Aim for a concise 3-to-5-paragraph explanation. | Medium |
| Provide a comprehensive and detailed breakdown, 600-800 words. | Long |

---

## 3-QUESTION CONTEXT FILTER

Before drafting any prompt, answer these:

1. **Who am I** in this situation? (role, relationship to audience)
2. **What does success look like?** (specific, measurable outcome)
3. **What are my constraints?** (deadline, audience, format, tools, budget)

If you can't answer all three, your prompt isn't ready.

---

## POWER FOLLOW-UPS

- **"Elaborate on points 2 and 3."** – deepen specific sections without rewriting everything.
- **"Critique this as a skeptical [role]. What are the weak points or missing pieces?"** – fast red team.
- **"Rewrite section 4 in a more [tone] style."** – targeted rewrites instead of starting over.

---

## COMMON MISTAKES

| Mistake | Fix |
|---------|-----|
| No task verb | Start with a specific action verb + end goal |
| Vague format | Specify exact structure: columns, sections, length |
| No verbosity control | Append a verbosity phrase |
| Over-specified steps for agentic | Describe the outcome, not the process |
| Giant custom instructions | Keep lean; control per prompt instead |

---

## CREDIT USAGE ESTIMATES (Perplexity Computer)

| Complexity | Typical Credits | Example |
|------------|----------------|---------|
| Simple (1-2 sub-agents) | 50–200 | Single-format report |
| Medium (3-5 sub-agents) | 200–800 | Multi-section report with charts |
| Complex (5+ sub-agents) | 800–2,000+ | Full deliverable package with visuals |

---

## EVALUATION RUBRICS

> For detailed rubric templates → 04_Tool_Rubrics_Addition.md

Quick quality check for any output:

| Dimension | Score 1-5 |
|-----------|-----------|
| Task completion (did it do what was asked?) | |
| Accuracy (facts, logic, sources) | |
| Format compliance (structure matches spec) | |
| Tone match (voice, audience fit) | |
| Actionability (can I use this immediately?) | |

**Threshold:** If any dimension < 3, iterate before accepting.
