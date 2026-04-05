```
# PROMPT DATABASE v3
> Battle-tested prompts organized by USE CASE.
> Storage target for post-output step 4: SAVE IT.
> Last updated: 2026-04-02

---

## HOW TO USE

1. After a productive AI conversation, run **Prompt Reversal**:
   > "Reverse-engineer our conversation into a single prompt. Output in a code block."
2. Paste into the appropriate USE CASE section below.
3. Tag with the 4 required fields. Add optional fields only if useful.
4. **Weekly review:** Test all `Captured` prompts with 3 diverse inputs. Promote to `Battle-Tested` or `Retire`.

### Entry Template (copy-paste)

```markdown
### [Prompt Name]
- **Status:** Captured | Battle-Tested | Retired
- **Target AI:** Standard LLM | Agentic AI
- **Model:** [model name]
- **Last Used:** [date]
- Optional: Tested with [N] inputs | Credit cost: [N] | Success Rate: [Pass/Partial/Fail]
- **Notes:** [one line — what it does, when to use it, edge cases]

> [paste reversed prompt here]
```

---

## USE CASE: RESEARCH & ANALYSIS

### Market Research Report Generator
- **Status:** Battle-Tested
- **Target AI:** Agentic AI
- **Model:** Perplexity Computer (Claude Opus 4.6 primary)
- **Last Used:** March 2026
- Credit cost: ~1,500 | Success Rate: Pass

> ```xml
> <role>Act as a senior market analyst with 15 years in B2B SaaS.</role>
> <outcome>Generate a 15-page PDF market research report on [TOPIC] including:
> executive summary, market size & growth, competitive landscape table (top 10 players
> with pricing/features/differentiators), trend analysis, and 3 strategic recommendations.</outcome>
> <constraints>
> - Sources published after 2024 only
> - Cross-reference all statistics with original sources
> - If data is unavailable, state "Data gap"
> - Do not exceed 15 pages
> - Credit budget: max 1,500
> </constraints>
> <format>Professional PDF with data tables, charts, and executive summary.</format>
> ```

---

### Deep-Dive Topic Synthesizer
- **Status:** Battle-Tested
- **Target AI:** Standard LLM
- **Model:** Claude Opus 4.6
- **Last Used:** March 2026
- Tested with 5 inputs | Success Rate: Pass

> ```xml
> <persona>You are a senior researcher who writes for informed but non-specialist audiences.</persona>
> <context>I need to quickly understand [TOPIC] at a working-knowledge level for [PURPOSE].</context>
> <task>Synthesize the current state of [TOPIC]. Cover: key concepts, major players/frameworks,
> recent developments (2024-2026), open debates, and practical implications for [MY ROLE].</task>
> <format>
> 1. TL;DR (3 bullets)
> 2. Core Concepts (brief definitions)
> 3. Current Landscape (who/what matters)
> 4. What's Changing (recent shifts)
> 5. So What? (implications for me)
> </format>
> <tone>Clear, direct, evidence-based.</tone>
> Think hard about this.
> ```

---

### NotebookLM Research Pack Builder — Mixed-Method UX
- **Status:** Captured
- **Target AI:** Standard LLM (Perplexity Space)
- **Model:** Perplexity Space (default model)
- **Last Used:** 2026-04-02
- **Notes:** Builds NotebookLM-ready source packs from mixed-method research studies (interviews + surveys + analytics) using a 6-bucket file system. Outputs: study overview, methods, data inventory, literature digest, synthesis, and NotebookLM pack.

> ```xml
> <persona>
> You are a mixed-methods UX research assistant.
> You prepare high-integrity, citation-aware, NotebookLM-ready research packs
> from uploaded study materials and verified web research.
> </persona>
>
> <context>
> This Space supports research studies that pair qualitative and quantitative
> data (interviews, documents, surveys, analytics).
> Source buckets:
> - 00_Study_Overview — brief, objectives, hypotheses, stakeholders
> - 01_Methods_Protocol — protocol, discussion guide, survey instrument
> - 02_Raw_Data — transcripts, field notes, survey exports, analytics
> - 03_Background_Literature — papers, reports, prior studies
> - 04_Synthesis — themes, evidence table, quote bank, synthesis memo
> - 05_NotebookLM_Ready — cleaned, import-ready source packs
> Use uploaded materials first.
> Use web research only to fill explicit evidence gaps or validate key claims.
> </context>
>
> <task>
> For each request:
> 1. Separate quantitative findings (metrics, distributions, segments)
>    from qualitative findings (themes, quotes, stories).
> 2. Synthesize both — where they converge, conflict, or leave gaps.
> 3. Preserve source labels, uncertainty, and direct quotes exactly.
> 4. Label all output: [FINDING], [INFERENCE], [OPEN QUESTION].
> 5. Produce NotebookLM-ready outputs: study memos, evidence tables,
>    theme summaries, quote banks, literature digests, analytics summaries,
>    and open-question lists.
> 6. Never fabricate missing context. State gaps explicitly.
> </task>
>
> <format>
> - Goal
> - Sources used
> - Key findings (quant + qual separated, then integrated)
> - Evidence
> - Contradictions or uncertainty
> - NotebookLM-ready deliverable
> - Gaps / next sources needed
> </format>
>
> <tone>Direct, analytical, cautious, citation-first. No hype.</tone>
> ```

---

## USE CASE: WRITING & DOCUMENTS

### Red-Team-Hardened Document Drafter
- **Status:** Battle-Tested
- **Target AI:** Standard LLM
- **Model:** Claude Opus 4.6
- **Last Used:** March 2026
- Tested with 3 inputs | Success Rate: Pass

> ```xml
> <persona>You are a senior [DOMAIN] specialist with 20 years of experience.</persona>
> <context>
> 1. My role: [ROLE]
> 2. Success looks like: [SPECIFIC OUTCOME]
> 3. Constraints: [AUDIENCE, DEADLINE, REQUIREMENTS]
> </context>
> <task>Draft a [DOCUMENT TYPE] that [SPECIFIC PURPOSE]. Structure it as [OUTLINE].</task>
> <exemplars>Follow the structure of the attached sample. Use [FRAMEWORK] format.</exemplars>
> <format>[EXACT OUTPUT STRUCTURE]</format>
> <tone>[2-3 specific words, e.g., "Professional, direct, evidence-based"]</tone>
>
> Before you begin, develop an internal rubric for world-class work for this type of output.
> Generate 3 diverse mock inputs to test your approach (Monte Carlo testing).
> Refine until outputs score 10/10. Show only the final version.
>
> Then: act as the toughest critic for this output. What are the immediate objections
> and weak points? Rewrite the weakest sections to withstand that scrutiny.
>
> Think carefully about this.
> ```

---

## USE CASE: ADVOCACY & LEGAL

*[empty — add first prompt here]*

---

## USE CASE: EMAILS & COMMUNICATION

*[empty — add first prompt here]*

---

## USE CASE: DATA & SPREADSHEETS

*[empty — add first prompt here]*

---

## USE CASE: PRESENTATIONS & DECKS

*[empty — add first prompt here]*

---

## USE CASE: PLANNING & STRATEGY

*[empty — add first prompt here]*

---

## USE CASE: PERPLEXITY COMPUTER WORKFLOWS

### Space Audit Prompt
- **Status:** Battle-Tested
- **Target AI:** Standard LLM (Perplexity Space context)
- **Model:** Claude Opus 4.6
- **Last Used:** March 2026
- Tested with 1 input | Success Rate: Pass

> ```
> Search all threads in the prompt lab space and give me a detailed
> recommendations on improvements to the space.
> ```
> **Notes:** Simple but effective. The space files provide all context needed.
> Works because the AI reads all space files and cross-references for gaps,
> redundancy, and missing patterns.

---

## USE CASE: PROMPT ENGINEERING (META)
### map [domain] — Taxonomy Builder Shortcut
- **Status:** Captured
- **Target AI:** Agentic AI
- **Model:** Perplexity Pro / Space
- **Last Used:** 2026-04-04
- **Notes:** One-word command shortcut. Type `map [domain]` to generate a complete outcomes-based taxonomy-builder prompt for any profession. 5 stored presets (audit, research, legal, education, history). Unknown domains auto-inferred. Updated `<format>` block enforces stable CSV naming: `{Domain}-Taxonomy-[label]` for collision-safe downstream routing.
- **Source file:** `map-shortcut-updated.md` (Space file)


*[empty — add first prompt here]*

---

## USE CASE: [ADD YOUR OWN]

*[empty — add first prompt here]*

---

## WORKFLOW TEMPLATES

```markdown
### NotebookLM Research Pack — End-to-End Workflow
- **Total micro-tasks:** 6
- **Manual tasks:** Fill study brief; design protocol; run fieldwork; collect raw data
- **AI-assisted tasks:** Literature digest; theme extraction; evidence table;
  quote bank; synthesis memo; NotebookLM pack assembly
- **Estimated time saved:** 4–6 hours per study
- **Target AI:** Standard LLM (Perplexity Space)
- **Estimated credits:** Low (Space-based, no Computer required)

Buckets and files:
- 00_Study_Overview → `STUDY_[topic]_overview`
- 01_Methods_Protocol → `METHOD_[topic]_protocol`
- 02_Raw_Data → `DATA_[topic]_[source]_[batch]`
- 03_Background_Literature → `LIT_[topic]_background`
- 04_Synthesis → `SYNTH_[topic]_themes_v01`, `SYNTH_[topic]_evidence_table`
- 05_NotebookLM_Ready → `NBLM_[topic]_[pack-name]` (10-source NotebookLM pack)

Workflow:
1. Planning thread → initial `<research_prompt>` → fill 00 + 01 in Space.
2. Same thread → file-list prompt → define all STUDY_ / METHOD_ / DATA_ / LIT_ / SYNTH_ / NBLM_ files.
3. Fieldwork → update 02 (Data Inventory, logs) and 03 (Literature digests).
4. Synthesis thread → 04 prompt + 04_Synthesis template → generate structured themes, evidence table, quote bank, memo.
5. Packaging thread → 05 prompt + 05_NotebookLM_Ready template → generate 10 NotebookLM-ready sources and pack manifest.
6. Upload 10 sources into a NotebookLM notebook named `[Study Name] — [YYYY-MM-DD]`;
   run the upload checklist (PII removed; labels present; no raw CSV; file size OK).
```

---

## TESTING LOG (Monte Carlo Validation)

```markdown
### Prompt Name — Date Tested
Mock Input 1: [describe] → Result: Pass|Partial|Fail → Notes: [what happened]
Mock Input 2: [describe] → Result: Pass|Partial|Fail → Notes: [what happened]
Mock Input 3: [describe] → Result: Pass|Partial|Fail → Notes: [what happened]
Overall: [N]/3 passed → Action: Promote | Refine | Retire
```

---

## SWIPE FILE INDEX

| # | Source Description | Use Case | Target AI | File Location |
|---|-------------------|----------|-----------|---------------|
| 1 |                   |          |           |               |

> When using swipe files: *"Analyze the attached examples. Identify key patterns in structure, tone, and persuasion. Apply to my content."*

---

## CREDIT TRACKING LOG

| Date | Prompt Name | Use Case | Credits Used | ROI Notes |
|------|-------------|----------|--------------|----------|
|      |             |          |              |          |
| **Monthly Total** | | | /10,000 | |

```
