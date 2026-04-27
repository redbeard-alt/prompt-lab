# Quick Commands Reference
## Prompt Lab — Quick Commands v1.1

> Attach this file to your Prompt Lab Space. Type any command keyword to trigger the workflow.

---

## How It Works

Type the **command keyword** (case-insensitive) as your entire message or at the start of your message. The AI detects the keyword and executes the associated workflow automatically.

Commands that accept arguments use the format: `COMMAND argument`

---

## Command Registry

| Command | Arguments | What It Does |
|---|---|---|
| `HAND OFF` | `--no-verify` (optional) | Generates a full thread handoff package for continuing work in a new thread |
| `RED TEAM` | none | Flips persona, attacks weak points in the last output |
| `FIX` | none | Rewrites the weakest sections based on the last RED TEAM |
| `REVERSE-ENGINEER` | none | Produces a single one-shot prompt that recreates the final output |
| `SAVE` | none | Stores the last reversed prompt in 05_Store by USE CASE |
| `AMPLIFY` | none | Spins the last output into other formats |
| `/map` | `domain` (required) | Generates an outcomes-based taxonomy prompt for the given domain |

---

## HAND OFF

**Trigger:** Type `HAND OFF` or `HAND OFF --no-verify`

**Purpose:** Generate everything needed to continue this thread's work in a fresh thread with zero context loss.

**Behavior when detected:**

Act as a meticulous project continuity specialist who treats thread handoffs like shift changes in an operating room — nothing gets lost.

### Mode Selection
- **Default (`HAND OFF`):** Execute Phase 1 (draft & verify), wait for user confirmation, then generate Phase 2.
- **Fast mode (`HAND OFF --no-verify`):** Skip Phase 1. Generate Phase 2 immediately using best extraction.

### Phase 1: Draft & Verify (skip if --no-verify)

Output a quick-reference checklist of:
- Every key decision or constraint established in this thread
- Which 2-3 of those are the MOST CRITICAL (user will confirm or override)
- Every file created, referenced, or modified (with version/status)
- Top abandoned approaches the new thread might re-attempt (max 5)
- Thread metadata: turn count, approximate duration, complexity (light / moderate / deep), refinement cycles completed

Then STOP and ask: "Anything missing, wrong, or out of date? Are the Critical Path items correct?"
Only proceed to Phase 2 after user confirms.

### Phase 2: Generate Two Documents

**Document 1: HANDOFF_CONTEXT.md**

Open with metadata block:
```
Generated: [YYYY-MM-DD HH:MM timezone]
Thread Complexity: [light / moderate / deep]
Turn Count: [N]
Refinement Cycles: [N]
⚠️ If more than 48 hours have passed since generation, re-verify the
Attachment Checklist and Active Constraints before proceeding.
```

Then these sections:

1. **Project Summary** — What we're building/doing, in 2-3 sentences.
2. **Critical Path** — 2-3 bullets max. The most important decisions or constraints that override all other context if there's any ambiguity. Confirmed by user in Phase 1.
3. **Key Decisions Made** — Bulleted list. Each bullet: the decision + brief rationale.
4. **Dead Ends & Rejected Approaches** (max 5 most consequential) — What was tried, why it failed or was abandoned. Include only approaches the new thread is likely to re-attempt. Omit trivial corrections.
5. **Current State** — What's done, what's in progress, immediate next step.
6. **Active Constraints** — Non-negotiable rules, boundaries, formatting requirements, or personas still in effect.
7. **Open Questions** — Unresolved issues, known gaps, pending user decisions.
8. **Files & Artifacts Registry** — Table:
   | Filename | Version | Status (final / in-progress / superseded) | What Changed Last |
9. **Attachment Checklist** — Bulleted list of every file the user must attach to the new thread alongside HANDOFF_CONTEXT.md. If no additional files, state "No additional attachments needed."

**Document 2: HANDOFF_PROMPT.md**

A single copy-paste prompt in a code block. Structure:

Open with Pre-Flight checklist:
```
## Pre-Flight (complete before sending)
- [ ] Filled in <target_environment> below
- [ ] Attached all files from the Attachment Checklist in HANDOFF_CONTEXT.md
- [ ] Will verify the AI passes all 3 challenge questions before continuing
```

Then target environment block (user fills in before pasting):
```
<target_environment>
  platform: [Perplexity Space / Perplexity Pro / ChatGPT / Claude / Other]
  model: [model name or "default"]
  space: [Space name or "none"]
</target_environment>
```

Then platform-conditional behavior rules:
```
Adapt your behavior to the target environment:
- If platform is ChatGPT or Claude: use explicit format tags and exemplars
  in all outputs. Structure matters — always specify output format.
- If platform is Perplexity Space: reference Space files by name. Follow
  Space Instructions if present.
- If platform is Perplexity Pro with tools: use outcome-based instructions.
  Do not specify steps. Let the orchestrator pick tools and models.
```

Then the body which must:
- Reference HANDOFF_CONTEXT.md as an attached file
- Copy the original persona block VERBATIM into the prompt. Do not summarize, paraphrase, or rewrite persona definitions — reproduce them exactly as they appeared in this thread.
- Re-establish task scope, active constraints, and format
- State the thread complexity tier so the new thread calibrates depth accordingly (light = keep responses concise; moderate = standard depth; deep = expect nuance, maintain all accumulated context carefully)
- Explicitly state: "The DEAD ENDS section lists rejected approaches. Do not revisit any of them unless I explicitly ask you to."
- Explicitly state: "The CRITICAL PATH items override all other context if there's any ambiguity."
- Specify where to pick up: current state + immediate next step

End with the **three-gate handoff protocol**:

**Gate 1 — Verification (must pass before proceeding):**
```
Before continuing, prove you've internalized the handoff context:
1. What is the immediate next step and why?
2. Name one rejected approach from Dead Ends and explain why it was abandoned.
3. What is the single highest-risk thing that could go wrong in the next
   step, and how do the active constraints prevent it?

Tailor these questions to the project:
- Code projects: Q3 should test architecture decisions and edge cases.
- Creative work: Q3 should test tone/audience/voice constraints.
- Analytical work: Q3 should test methodology and data constraints.
The questions must require reasoning, not recall.
```

**Gate 2 — Verification failure protocol:**
```
If any answer is wrong or incomplete:
(1) I will correct you.
(2) Re-read the attached HANDOFF_CONTEXT.md.
(3) Re-answer only the failed question(s).
(4) Do not proceed to work until all 3 pass.
```

**Gate 3 — Clarification window (after verification passes):**
```
After passing all 3 verification questions, ask any clarifying questions
you have about the handoff context — one at a time. Do not bundle multiple
questions into a single message. Do not begin work until I say "go" or
confirm there are no more questions to answer.
```

Output both documents in full. No placeholders — fill in everything from the actual conversation.

---

## RED TEAM

**Trigger:** Type `RED TEAM`

**Behavior:** Flip persona to the toughest critic for the last output (e.g., skeptical executive, opposing counsel, demanding client). You have 60 seconds to review. List immediate objections, weak points, and reasons to dismiss — be specific. Rank by severity. End by offering FIX as next step.

---

## FIX

**Trigger:** Type `FIX`

**Behavior:** Based on the weaknesses identified in the last RED TEAM, rewrite the weakest sections to withstand that scrutiny. Show only changed sections with a change tracker table.

---

## REVERSE-ENGINEER

**Trigger:** Type `REVERSE-ENGINEER`

**Behavior:** Reverse-engineer the entire conversation into the single prompt that would have produced the final output in one shot. Output in a code block. No preamble.

---

## SAVE

**Trigger:** Type `SAVE`

**Behavior:** Store the last reversed prompt in 05_Store_Prompt_Database.md under the appropriate USE CASE category. Tag with: Name, Status (Captured), Target AI, Model, Date.

---

## AMPLIFY

**Trigger:** Type `AMPLIFY`

**Behavior:** Offer to spin the last strong output into:
- Summary for a different audience
- Talking points for a meeting
- Short timeline or checklist
- Email or memo
- Presentation outline

User picks which formats. Only amplify high-quality source material.

---

## /map

**Trigger:** Type `/map domain`

**Behavior:** See map-shortcut-updated.md for full implementation. Generates an outcomes-based taxonomy-builder prompt for the given domain.

---

## Adding New Commands

To add a command:
1. Pick a short, memorable keyword (1-2 words or `/slash` format)
2. Add it to the Command Registry table
3. Write the full behavior specification in its own section below the table
4. Test with 3 diverse inputs before marking Battle-Tested

---

## Version History

| Version | Date | Changes |
|---|---|---|
| v1 | 2026-04-13 | Initial release. Commands: HAND OFF, RED TEAM, FIX, REVERSE-ENGINEER, SAVE, AMPLIFY, /map |
| v1.1 | 2026-04-13 | HAND OFF: Added Gate 3 clarification window (one question at a time, explicit "go" gate). Added Critical Path confirmation to Phase 1. Three-gate protocol structure. |
