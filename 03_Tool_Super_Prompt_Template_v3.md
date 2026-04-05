# PROMPT LAB: SUPER-PROMPT TEMPLATES v3
> Copy-paste. Fill in the brackets. Ship it.
> For framework details → 01_Core | For lookup tables → 04_Tool | For debugging → 06_Troubleshooting
> Last updated: March 2026

---

## WHICH TEMPLATE?

| If your target is… | Use |
|--------------------|-----|
| ChatGPT, Claude, Gemini (single-turn chat) | **Template A** |
| Perplexity Computer, multi-agent systems | **Template B** |
| Not sure? → see 00_Index Decision Tree | |

---

## TEMPLATE A — STANDARD LLM (6-Part Formula)

> For framework theory → 01_Core Part 2
> For specialized frameworks (MAGIC, CARE, DIG, SCQA, SPARSPARK) → 01_Core Part 2

```xml
<persona>
You are a [ROLE] with [X] years of experience in [DOMAIN].
</persona>

<context>
1. My role: [WHO I AM in this situation]
2. Success looks like: [SPECIFIC MEASURABLE OUTCOME]
3. Constraints: [DEADLINES, AUDIENCE, LIMITATIONS, TOOLS]
Materials provided: [LIST any attached files, links, or reference docs]
</context>

<task>
[ACTION VERB] + [SPECIFIC END GOAL].

First, [ANALYZE / REVIEW / RESEARCH] the [MATERIALS / TOPIC] for [SPECIFIC FOCUS].
Then, [DRAFT / CREATE / BUILD] a [DOCUMENT TYPE] that [SPECIFIC PURPOSE].
Finally, [IDENTIFY / RECOMMEND / FLAG] [GAPS / RISKS / NEXT STEPS].
</task>

<exemplars>
[Choose one or more:]
- Follow the structure of the attached sample.
- Use the [FRAMEWORK NAME] format (e.g., STAR, SWOT, MECE).
- Analyze the attached examples. Identify key patterns in structure,
  tone, and persuasion. Apply those patterns to my content.
</exemplars>

<format>
[EXACT OUTPUT STRUCTURE. Pick or customize:]
1. TL;DR in 3-5 bullets
2. Table with columns: [COL A], [COL B], [COL C]
3. Timeline: chronological narrative
4. Email: Subject → Opening → Key Points → CTA
5. Report: Executive Summary → Analysis → Findings → Recommendations
6. [YOUR CUSTOM STRUCTURE — be surgical]
</format>

<tone>
[Pick 2-3 specific words, e.g.:]
- Professional and direct
- Warm yet authoritative
- Concise and evidence-based
- Clear, confident, and friendly
</tone>
```

### Optional Add-ons (append after closing tags)

```
QUALITY GATE (for high-stakes outputs):
Before you begin, develop an internal rubric for world-class work for this
type of output. Generate 3 diverse mock inputs to test your approach
(Monte Carlo testing). Refine until outputs score 10/10. Show only the
final version.

ROUTER NUDGE (pick one based on complexity → see 04_Tool):
Think hard about this.
Think deeply about this.
Think carefully about this.

VERBOSITY CONTROL (pick one → see 04_Tool):
Give me the bottom line in 100 words or less. Use markdown.
Aim for a concise 3-to-5-paragraph explanation.
Provide a comprehensive and detailed breakdown, 600-800 words.
```

---

## TEMPLATE B — AGENTIC AI (Perplexity Computer / Outcomes-Based)

> For strategy details → 02_Core Part 3
> For credit optimization → 02_Core Part 4 or 04_Tool
> ⚠ DO NOT specify steps, tools, or process. Describe the outcome only.

```xml
<role>
Act as a [EXPERT PERSONA, e.g., Senior Market Analyst with 15 years in B2B SaaS].
</role>

<outcome>
Generate a [SPECIFIC DELIVERABLE, e.g., 15-page PDF report / live web application]
about [TOPIC] including:
- [COMPONENT 1]
- [COMPONENT 2]
- [COMPONENT 3]
</outcome>

<constraints>
- Rely only on [SOURCE TYPES, e.g., peer-reviewed papers / SEC filings / .gov sites]
- Cross-reference all claims
- If data is unavailable, state "Data gap"
- Do not exceed [X PAGES / WORDS]
- Credit budget: max [N] credits
</constraints>

<format>
Format with [STYLING REQUIREMENTS, e.g., professional styling, data tables,
executive summary, charts, section headers].
</format>

<delivery>
Deliver the final output to [CONNECTOR DESTINATION, e.g., my connected
Google Drive folder / Slack channel / as downloadable file].
</delivery>
```

---

## POST-OUTPUT PROMPTS (copy-paste after any strong result)

Run in order. Skip any that don't apply.

### 1. RED TEAM

```
Now act as the toughest critic for this output (e.g., skeptical executive,
opposing counsel, demanding client). You have 60 seconds to review this.
What are your immediate objections, weak points, and reasons to dismiss it?
Be specific.
```

### 2. FIX

```
Based on the weaknesses you identified, rewrite the three weakest sections
to withstand that scrutiny.
```

### 3. REVERSE-ENGINEER

```
Reverse-engineer our entire conversation and write the single prompt that
would have produced this final response in one go. Output it in a code block.
```

### 4. SAVE

```
Store this reversed prompt in 05_Store under the appropriate USE CASE category.
Tag with: Name, Status (Captured), Target AI, Model, Date.
```

### 5. AMPLIFY

```
Spin this output into the following formats:
- [Summary for a different audience]
- [Talking points for a meeting]
- [Short timeline or checklist]
- [Email or memo]
- [Presentation outline]
(Pick the ones you need. Delete the rest.)
```

> **Rule:** Only amplify HIGH-QUALITY source material. AI magnifies whatever you feed it.

---

## SPECIALIZED FRAMEWORK STARTERS (quick-launch, details in 01_Core Part 2)

### DIG (Data Analysis)
```
<task>
1. Description: Give me the lay of the land for [DATASET/TOPIC].
2. Introspection: Surface the 5 most valuable questions this data can answer.
3. Goal Setting: Recommend which analysis to prioritize and why.
</task>
```

### SCQA (Presentations)
```
<task>
Structure a presentation outline using SCQA:
- Situation: [CURRENT STATE]
- Complication: [WHAT CHANGED / PROBLEM]
- Question: [WHAT WE NEED TO ANSWER]
- Answer: [PROPOSED SOLUTION / RECOMMENDATION]
</task>
```

### SPARSPARK (Negotiations)
```
<task>
Help me prepare for a negotiation:
1. Sharpen: Clarify my position on [TOPIC]
2. Probe: Map the counterparty's likely concerns and motivations
3. Attack: Red-team my own position — what are my weakest points?
4. Rehearse: Give me 3 likely objections and strong responses for each
</task>
```

### Swipe File Protocol (Style Matching)
```
Analyze the attached examples. Identify key patterns in structure, tone,
and persuasion. Apply those patterns to my content below:

[PASTE YOUR CONTENT]
```

---

## Scope Note

This file defines **prompt templates only**. Do not embed real shell commands here. If a template needs command behavior, reference the relevant entry in Terminal Lab instead of pasting the command body.
