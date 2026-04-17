# Red Team Notes — Chapter Trio Builder v1

**Target prompt:** `v1-original.md`
**Red team date:** Apr 17, 2026
**Reviewer persona:** Hostile QA engineer trying to break the prompt in production.
**Result:** 20 distinct failure modes. Top 3 are blockers; the prompt should not be used as-is for any chapter other than Ch. 15.

---

## Critical Failures (prompt produces wrong output or crashes)

### 1. Hardcoded "11 sources" is a lie for most chapters
Step 5 states "add 11 sources," but step 2 says "1–2 videos per section" and OpenStax chapters have 3–7 sections.
- 3-section chapter × 1 video = 9 sources
- 6-section chapter × 2 videos = 17 sources
The agent will either pad with filler or skip real content to hit 11.
**Fix:** Compute `source_count = (# sections + 1 intro) + (# videos chosen) + 1 answer key`. State as formula, not a magic number.

### 2. OpenStax URL patterns are assumed, not verified
`/{N}-summary` and `/{N}-key-terms` aren't always correct — OpenStax uses mixed slug patterns and section titles sometimes contain years (e.g., `15-3-1863-the-changing-nature-of-the-war`). No fallback if slug differs.
**Fix:** Require the agent to fetch the chapter index page and extract section URLs from the HTML, not construct them.

### 3. "Sequential-only" doc creation is fragile folklore
Based on a single observation during Ch. 14. May have been a transient Pipedream issue. Hardcoding SEQUENTIAL wastes ~60s per chapter forever.
**Fix:** Allow parallel, catch null, fall back to sequential only on failure.

### 4. Null-response retry has a race condition
`find-document` returns the most recent match. If a duplicate exists (happened in Ch. 14), the agent picks the wrong one.
**Fix:** Match on exact title AND creation timestamp > task start time.

### 5. No handling for OpenStax fetch failures
If openstax.org is down or rate-limits, the agent silently hallucinates section titles from memory. Single most dangerous failure for an educational product.
**Fix:** Require fetch-success confirmation before any markdown is written. Fail loudly if unavailable.

---

## Content Quality Failures

### 6. Preferred-channels list is stale
Channels get demonetized, videos get removed, and "Daily Dose of History" 3-min format is too shallow for some topics. No verification the video actually covers the section.
**Fix:** Require the agent to read the video description or transcript snippet and confirm topical match.

### 7. "1a/1b/2a/2b formatting" assumes every question has sub-parts
Real chapters have atomic questions too. Forcing sub-parts on everything creates padding.
**Fix:** "Use 1a/1b only when a question has genuine sub-parts; use 1, 2, 3 for atomic questions."

### 8. No word-count or cognitive-load ceiling
A 14-section chapter becomes 28 questions and 20 vocab terms. No pruning guidance. Ch. 15 worked because it had 4 sections.
**Fix:** Cap at 8–12 questions per chapter and 12–15 key terms; if OpenStax has more, select the most exam-relevant.

### 9. "Common confusions" and "ACT/SAT exam tip" are invented
The agent has no source for these — generated from memory. For a homeschool-compliance context, this is a fact-checking liability.
**Fix:** Require a citation or rename to "suggested watch-outs" to flag that the parent should verify.

### 10. Sensitivity-language rule only covers one domain
Only addresses enslaved-people terminology. Doesn't cover Indigenous nations, Japanese American incarceration, "War Between the States" vs "Civil War," etc.
**Fix:** Link to a style guide file rather than enumerate one example.

---

## Operational / Workflow Failures

### 11. "Deliver in one final message" conflicts with async browser_task
Browser tasks run 5–15 min. If the user leaves, the final message never ships.
**Fix:** If browser_task > 10 min, deliver partial results (3 Docs) and note NotebookLM is still building.

### 12. No versioning / idempotency
Running twice for the same chapter creates 6 Docs and 2 NotebookLMs.
**Fix:** Before creating, call `find-document` by title; if exists, prompt user to overwrite or increment to v2.

### 13. No rollback on partial failure
If Answer Key creates but NotebookLM fails, workspace is half-built.
**Fix:** Explicit cleanup instructions or at minimum a "what got built" status report regardless of outcome.

### 14. browser_task instructions hardcode "11 sources" again
Same bug as #1, propagated into the subagent. When actual count is 9, the subagent thinks something is wrong and retries.

### 15. No user-approval timeout for local browser
`use_local_browser={local:true}` pops a permission dialog. If user is AFK, task hangs indefinitely.
**Fix:** Add timeout + fallback to cloud browser after 5 min.

---

## Structural / Prompt-Engineering Failures

### 16. `<INPUTS_TO_FILL>` is at the bottom
Standard practice: inputs go at top so the executor resolves them first.
**Fix:** Move `<INPUTS>` above `<CONTEXT>`.

### 17. `<QUALITY_BAR>` duplicates `<FORMAT>` and `<WORKFLOW>` items
"Source count = 11" appears in step 5, FORMAT, and QB. Redundancy creates drift.
**Fix:** Single source of truth per rule.

### 18. No failure mode for "chapter doesn't exist"
Ch. 30 of a 29-chapter book. Agent hallucinates.
**Fix:** Validate N ≤ 29 up front.

### 19. No token / cost budget
Spawns a subagent + 3 large Docs + 5–15 min browser task. 10k+ tokens, significant credits. No runaway detection.
**Fix:** Add `<BUDGET>max 2 subagents, max 1 browser_task, max 15 min total</BUDGET>`.

### 20. No user-verifiable success criteria
"All 4 assets delivered" isn't a 30-second QA checklist.
**Fix:** Acceptance criteria = "Open each link; verify (a) Docs render correctly, (b) NotebookLM source count matches formula, (c) Teaching Notes name Ch. {N-1} and Ch. {N+1}."

---

## Top 3 to Fix First

| Rank | Issue | Why it's #1–3 |
|---|---|---|
| 1 | Hardcoded "11 sources" (#1, #14) | Breaks on every chapter that isn't Ch. 15 |
| 2 | Assumed OpenStax URLs (#2) + no fetch-failure handling (#5) | Silent hallucination → fake educational content |
| 3 | No idempotency / duplicate handling (#12) | Already bit Ch. 14 build; will bite again |

---

## All 20 Addressed in `v2-fixed.md`
Every issue above is explicitly resolved in v2. Cross-reference the `<CHANGE_LOG>` section of v2 for one-line-per-issue traceability.
