# OpenStax U.S. History — Chapter Trio Builder (v2, FIXED)

**Use case:** Homeschool / Curriculum Build
**Author:** Prompt Lab
**Supersedes:** `v1-original.md`
**Resolves:** All 20 issues in `red-team-notes.md`.

---

```
<INPUTS>
- {N} = chapter number. Must be an integer 1 ≤ N ≤ 29 (OpenStax U.S. History has 29 chapters). If N is out of range, STOP and report.
- {Chapter Title} = exact OpenStax chapter title. If not provided, fetch it from the OpenStax TOC in step WF-1 before proceeding.
</INPUTS>

<TASK>
Build the 4-asset OpenStax U.S. History chapter trio for Chapter {N} for a 10th-grade homeschool student:
1) Video Guide + Section Questions (Google Doc)
2) Vocabulary Sheet — student copy (Google Doc)
3) Vocabulary ANSWER KEY — teacher copy (Google Doc)
4) NotebookLM notebook with all chapter sources loaded

Deliver the 4 links in a single final message, with graceful partial delivery if the NotebookLM build exceeds 10 minutes.
</TASK>

<CONTEXT>
- Student: 10th grader, Colorado independent-school homeschool pathway.
- Textbook: OpenStax U.S. History, https://openstax.org/books/us-history
- Google account (Docs + NotebookLM): admin@checschool.org (signed in on the local browser).
- Connectors: google_docs__pipedream (CONNECTED), local browser for NotebookLM.
- Sensitivity / style guide: SEE `<STYLE_GUIDE>` below — do not default to legacy terminology.
</CONTEXT>

<STYLE_GUIDE>
Use modern scholarly terminology. Never substitute.
- "enslaved people" (not "slaves"); "slaveholder" (not "master" / "owner")
- "Indigenous peoples" / specific nation name (not "Indians" except in direct quotes or proper nouns like "American Indian Movement")
- "Japanese American incarceration" (not "internment")
- "Civil War" (not "War Between the States")
- "Reconstruction-era Black codes" (not "negro codes")
- For anything else that could be sensitive, flag it in the Answer Key Teaching Notes as "terminology watch" and cite the OpenStax page used.
</STYLE_GUIDE>

<BUDGET>
- Max 1 research/subagent call
- Max 1 browser_task (with 10-min soft deadline; see WF-5)
- Max 15 min wall-clock total
- If any limit is hit, deliver partial results with status report.
</BUDGET>

<WORKFLOW>

WF-1. PRE-FLIGHT VALIDATION
- Validate 1 ≤ N ≤ 29. If not, STOP, report to user.
- Fetch https://openstax.org/books/us-history/pages/{N}-introduction. If fetch FAILS or returns non-200, STOP — do NOT hallucinate section titles. Report the failure to the user and ask whether to retry or abort.
- From the fetched intro page, extract the chapter's actual section URLs by parsing the in-page TOC / next-page links. Record: intro URL, each section URL, section titles, and count (call this S).
- Fetch the chapter's key-terms page. Try `/{N}-key-terms` first; if 404, search the chapter TOC for a page whose title contains "Key Terms". Record the list of official key terms (count = K).
- Check for duplicates: call google_docs-find-document with nameSearchTerm "Ch {N} — Video Guide". If any result exists, ASK USER: overwrite, make v2, or abort. Do the same for the other two target titles.

WF-2. VIDEO SELECTION (1 per section; optionally 2 when a section has a genuinely distinct second topic)
- For each of the S sections, pick ONE primary YouTube video. Optionally add a SECOND only when the section covers two distinct topics.
- Preferred channels (in order): Heimler's History, Crash Course US History, Khan Academy. Use Daily Dose of Documentaries / Simple History / OverSimplified ONLY for supplementary short-form; never as the primary.
- VERIFY TOPICAL MATCH: for each candidate, read the YouTube video title + description. If the description does not clearly cover the section's subject, pick a different video. Log the match check in a comment at the top of the Video Guide markdown.
- Capture: title, channel, runtime, full URL. Let V = total videos chosen.

WF-3. CONTENT CAPS (prevent cognitive overload)
- Questions: target 8–12 total across the chapter. Distribute proportionally to section length. Use 1a/1b ONLY when a question has genuine sub-parts; otherwise use plain 1, 2, 3.
- Key terms in student + answer sheets: cap at 12–15. If OpenStax lists more, select the most exam-relevant and note in Teaching Notes which were omitted and why.

WF-4. WRITE MARKDOWN FILES (workspace = /home/user/workspace/)
a. Ch{N}_Video_Guide.md — header comment listing each video's topical-match check; then section-by-section with linked section title → OpenStax URL, embedded video link(s), questions per WF-3, each followed by "*Answer:*" with blank lines.
b. Ch{N}_Vocabulary_Sheet.md — every chosen key term with blank definition space. Mark the first term with ★ (U+2605) and fill in its definition as the worked example. Include: Compare & Contrast (3 prompts), Self-Check matching (7 questions), one Short-Answer prompt.
c. Ch{N}_Vocabulary_ANSWER_KEY.md — full definitions with key phrases bolded; Compare & Contrast sample answers; Self-Check answers; Short-Answer scoring guide; Teaching Notes with:
   - "Connection back to Ch. {N-1}" (or "N/A — first chapter" if N=1)
   - "Connection forward to Ch. {N+1}" (or "N/A — final chapter" if N=29)
   - Key dates
   - "Suggested watch-outs" (NOT "common confusions"; this signals parent verification) — each with a citation URL
   - One "ACT/SAT-adjacent tip" — LABEL as "unofficial / parent to verify"

WF-5. GOOGLE DOCS (fastest safe path)
- Capture task_start_timestamp before any writes.
- Try ALL THREE create-document calls in parallel. Exact titles:
  * "Ch {N} — Video Guide & Section Questions (10th Grade US History · OpenStax)"
  * "Ch {N} — Vocabulary Sheet (10th Grade US History · OpenStax)"
  * "Ch {N} — Vocabulary ANSWER KEY — Teacher Copy (10th Grade US History · OpenStax)"
  All with useMarkdown: true.
- If a call returns a valid documentId, use it.
- If a call returns null, retry THAT ONE call sequentially. If still null, call google_docs-find-document with the exact title AND filter results to createdTime > task_start_timestamp; pick the matching doc. If no match, report the failure.
- Record all three document IDs.

WF-6. NOTEBOOKLM (browser_task, local browser, soft 10-min deadline)
- source_count = S + 1 (intro) + V + 1 (answer key) — compute and pass this to the subagent; do NOT hardcode a number.
- Spawn browser_task with use_local_browser={local:true, question:"Allow Computer to build the Chapter {N} NotebookLM in your admin@checschool.org Drive?"}. Include a 5-min user-approval timeout; if user doesn't approve in 5 min, fall back to cloud browser and proceed (Answer Key doc will still be added if NotebookLM can access Drive).
- Subagent task: create notebook titled "Chapter {N} — US History (10th Grade · OpenStax)"; add the computed sources (intro + S section URLs + V YouTube URLs + Answer Key Google Doc). Must return notebook UUID URL AND actual final source count.
- Soft deadline: if the browser_task exceeds 10 min wall clock, do NOT abort — continue to WF-7 with a "still building" marker for the NotebookLM row.

WF-7. PARTIAL-DELIVERY RULES
- At 10-min mark or when all 4 assets are done, assemble the final message per `<FORMAT>`.
- If NotebookLM is still running, include the 3 Doc links + a "NotebookLM still building — will share when ready" note, then continue polling and send a follow-up when done.
- If any Doc failed, include what succeeded and an explicit failure line naming the missing asset.

WF-8. ACCEPTANCE CHECKLIST (user-verifiable, 30 sec)
Print at the end of the final message:
- [ ] Each of the 3 Doc links opens in Google Docs with headings + bold rendering intact
- [ ] NotebookLM source count equals {S + 1 + V + 1} = N_sources
- [ ] Teaching Notes explicitly name Ch. {N-1} and Ch. {N+1} (or the N/A note if applicable)
- [ ] No placeholder text (`{N}`, `{Chapter Title}`, `TBD`) present anywhere
</WORKFLOW>

<FORMAT>
- Start every response with: `Task type: ACADEMICS`
- Typography (exact code points): em dash — (U+2014), middle dot · (U+00B7), star ★ (U+2605). Never substitute hyphen-minus or asterisk.
- Doc titles: `Ch {N} — {Asset} (10th Grade US History · OpenStax)`
- NotebookLM title: `Chapter {N} — US History (10th Grade · OpenStax)`
- Final delivery: 4-row Markdown table (Asset | Purpose | Link), followed by "What's in Ch. {N}" bullets, then the Acceptance Checklist from WF-8, then offer to continue to Ch. {N+1}.
</FORMAT>

<CHANGE_LOG>
Each entry = red-team issue number resolved.
1  → WF-6 uses formula `S + 1 + V + 1` instead of hardcoded 11.
2  → WF-1 extracts section URLs from the actual OpenStax TOC, not assumed slug pattern.
3  → WF-5 uses parallel-first with sequential fallback; not hardcoded sequential.
4  → WF-5 filters find-document results by createdTime > task_start_timestamp to avoid picking old duplicates.
5  → WF-1 STOPs on OpenStax fetch failure; no silent hallucination.
6  → WF-2 requires topical-match verification against each video's description.
7  → WF-3 restricts 1a/1b to genuine sub-parts; atomic questions stay flat.
8  → WF-3 caps questions at 8–12 and key terms at 12–15.
9  → WF-4c renames "common confusions" → "suggested watch-outs" with citations and labels the ACT/SAT tip as parent-verify.
10 → `<STYLE_GUIDE>` section replaces one-off enslaved-people rule with a full multi-domain list.
11 → WF-5/WF-7 adds partial-delivery path if NotebookLM > 10 min.
12 → WF-1 checks for existing docs and asks about overwrite / v2 / abort before creating duplicates.
13 → WF-7 partial-delivery rules ensure a status report even on half-build; next user run can reconcile.
14 → WF-6 passes the computed source_count to the browser_task; no "11" in the subagent prompt.
15 → WF-6 adds 5-min approval timeout + cloud-browser fallback.
16 → `<INPUTS>` moved to the top of the prompt.
17 → Removed the separate `<QUALITY_BAR>`; single source of truth is the workflow + `<FORMAT>` + acceptance checklist.
18 → WF-1 validates 1 ≤ N ≤ 29.
19 → `<BUDGET>` section added with subagent / browser / wall-clock ceilings.
20 → WF-8 acceptance checklist is user-verifiable in 30 seconds.
</CHANGE_LOG>
```
