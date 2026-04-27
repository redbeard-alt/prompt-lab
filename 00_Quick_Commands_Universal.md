# Quick Commands — Universal
## Cross-Space Quick Commands v1.1

> This file is auto-synced from `_shared/`. Do not edit in-place — edit the source at `$PXROOT/_shared/00_Quick_Commands_Universal.md` and re-run `sync-shared.sh`.

---

## How It Works

Type the **command keyword** (case-insensitive) as your entire message or at the start of your message. The AI detects the keyword and executes the associated workflow automatically.

Commands that accept arguments use the format: `COMMAND argument`

---

## Command Registry

| Command | Arguments | What It Does |
|---|---|---|
| `PATCH` | `<brief purpose>` (optional) | Converts an attached `PATCH_*.md` into a Terminal Lab execution package with prompt + attachment checklist |
| `HAND OFF` | `--no-verify` (optional) | Generates a full thread handoff package for continuing work in a new thread |
| `RED TEAM` | none | Flips persona, attacks weak points in the last output |
| `FIX` | none | Rewrites the weakest sections based on the last RED TEAM |

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
- Every file created, referenced, or modified (with version/status)
- Top abandoned approaches the new thread might re-attempt (max 5)
- Thread metadata: turn count, approximate duration, complexity (light / moderate / deep)

Then STOP and ask: "Anything missing, wrong, or out of date?"
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
2. **Critical Path** — 2-3 bullets max: the most important decisions/constraints that override everything else if there's ambiguity. User-confirmed in Phase 1.
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

Then conditional behavior rules based on target_environment:
- If platform is ChatGPT or Claude: use explicit format tags and exemplars in all outputs.
- If platform is Perplexity Space: reference Space files by name.
- If platform is Perplexity Pro with tools: use outcome-based instructions, do not specify steps.

Then the body which must:
- Reference HANDOFF_CONTEXT.md as an attached file
- Copy the original persona block VERBATIM (never summarize or paraphrase personas)
- Re-establish task scope, active constraints, and format
- State the thread complexity tier so the new thread calibrates depth
- State: "The DEAD ENDS section lists rejected approaches. Do not revisit any of them unless I explicitly ask you to."
- State: "The CRITICAL PATH items override all other context if there's any ambiguity."
- Specify where to pick up: current state + immediate next step

End with challenge-based verification:
```
Before continuing, prove you've internalized the handoff context:
1. What is the immediate next step and why?
2. Name one rejected approach from Dead Ends and explain why it was abandoned.
3. What is the single highest-risk thing that could go wrong in the next
   step, and how do the active constraints prevent it?
```

Then verification failure protocol:
```
If any answer is wrong or incomplete:
(1) I will correct you.
(2) Re-read the attached HANDOFF_CONTEXT.md.
(3) Re-answer only the failed question(s).
(4) Do not proceed to work until all 3 pass.
```

Tailor the three challenge questions to the project type:
- For code projects: test understanding of architecture decisions and edge cases.
- For creative work: test understanding of tone/audience/voice constraints.
- For analytical work: test understanding of methodology and data constraints.
The three questions must require reasoning, not recall.

Output both documents in full. No placeholders — fill in everything from the actual conversation.

### Phase 3: Archive Handoff

After outputting both documents, instruct the user to archive them to the handoff log:

**Naming convention:** `YYYY-MM-DD_short-description.md` and `YYYY-MM-DD_short-description_PROMPT.md`

Provide these paste-ready commands (substitute the actual date and a slug derived from the Project Summary):

```
export PXROOT="/Users/bryanjhein/Library/CloudStorage/Dropbox-Privaterelay/Bryan Hein/Perplexity"
mkdir -p "$PXROOT/_handoffs"
cp ~/Downloads/HANDOFF_CONTEXT.md "$PXROOT/_handoffs/YYYY-MM-DD_short-description.md"
cp ~/Downloads/HANDOFF_PROMPT.md "$PXROOT/_handoffs/YYYY-MM-DD_short-description_PROMPT.md"
```

Replace `YYYY-MM-DD` with the current date and `short-description` with a 2-4 word kebab-case slug summarizing the thread (e.g., `bootstrap-scaffold`, `warp-kb-build`, `promptlab-audit`).

Then suggest renaming the thread to match: `YYYY-MM-DD_short-description`.

---

## RED TEAM

**Trigger:** Type `RED TEAM`

**Behavior:** Flip persona to the toughest critic for the last output (e.g., skeptical executive, opposing counsel, demanding client). You have 60 seconds to review. List immediate objections, weak points, and reasons to dismiss — be specific. Rank by severity. End by offering FIX as next step.

---

## FIX

**Trigger:** Type `FIX`

**Behavior:** Based on the weaknesses identified in the last RED TEAM, rewrite the weakest sections to withstand that scrutiny. Show only changed sections with a change tracker table.

---

## Version History

| Version | Date | Changes |
|---|---|---|
| v1.2 | 2026-04-14 | Added PATCH command for cross-Space patch orchestration via Terminal Lab |
| v1 | 2026-04-13 | Initial release. HAND OFF, RED TEAM, FIX |
| v1.1 | 2026-04-14 | HAND OFF: added Phase 3 (archive to `_handoffs/`, rename thread) |

---

## PATCH

**Trigger:** Type `PATCH` or `PATCH <brief purpose>`

**Purpose:** Convert an attached `PATCH_*.md` file into a safe Terminal Lab execution package for Warp, including the exact attachments needed to apply the patch with verification.

**Behavior when detected:**

Act as a cross-Space patch coordinator. Do not apply the patch inline. Do not edit target files directly in the current Space.

### Inputs
- Required: one attached `PATCH_*.md` file
- Optional: target files named in the patch, if already attached
- Reference: `00_Space_Registry.md`

### Workflow

1. Parse the patch file and extract:
- Target Space
- Files to modify
- Edit type per file, append / replace / additive only
- Anchor sections or insertion points
- Verification checklist
- Any format contracts or table schemas being introduced

2. Resolve the target Space path using `00_Space_Registry.md`.

3. Determine required attachments for execution:
- Always include the patch file
- Include each target file if verification against live content is required
- If the patch changes shared contracts across Spaces, include any paired receiving/sending spec files named by the patch

4. Output a **Terminal Lab prompt** for Warp that tells Terminal Lab to:
- inspect the patch and target files
- dry-run anchors and matches first
- back up every file before mutation
- use safe macOS-compatible edit patterns
- make additive changes only unless the patch explicitly authorizes replacement
- produce a verification report at the end

5. Output an **Attachment Checklist** with exact filenames the user must attach in Terminal Lab.

### Output format

Produce exactly these sections:

#### Terminal Lab Prompt
A single copy-paste prompt intended for Terminal Lab. It must:
- name the target Space and resolved folder path
- name every target file with full path
- state the patch intent in 1-2 sentences
- instruct Terminal Lab to perform EXPLAIN → DRY-RUN → RED TEAM → HARDEN → APPLY → VERIFY
- require backups before edits
- require non-destructive previews before any state change
- require final verification against the patch checklist

#### Attachment Checklist
- Patch file
- Target files
- Any shared registry or contract files needed

#### Execution Notes
- Whether the patch is additive-only
- Whether any cross-Space contract changed
- Whether a follow-up sync is required

### Rules
- Never fabricate file paths; resolve them through `00_Space_Registry.md`
- Never apply the patch in the current thread
- Never omit the attachment checklist
- If target files are missing, still generate the Terminal Lab prompt, but explicitly mark validation as blocked until attachments are added
