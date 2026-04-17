# OpenStax U.S. History — Chapter Trio Builder (v1, ORIGINAL)

**Use case:** Homeschool / Curriculum Build
**Author:** Prompt Lab (reverse-engineered from CHEC Independent School session, Apr 17, 2026)
**Status:** Superseded by v2. Kept for history / diff reference.
**Known issues:** See `red-team-notes.md` in this folder — 20 failure modes catalogued.

---

```
<TASK>
Build the complete 4-asset OpenStax U.S. History chapter trio for Chapter {N} ("{Chapter Title}") for a 10th-grade homeschool student. Deliver all four links in one final message.
</TASK>

<CONTEXT>
- Student: 10th grader, Colorado independent-school homeschool pathway.
- Textbook: OpenStax U.S. History — https://openstax.org/books/us-history/pages/{N}-introduction
- Google account for all Docs + NotebookLM: admin@checschool.org (already signed in on the local browser).
- Connectors available: google_docs__pipedream (CONNECTED), local browser for NotebookLM.
- Language rule: always use "enslaved people" (not "slaves") and "slaveholder" (not "master").
</CONTEXT>

<WORKFLOW>
1. Fetch OpenStax Chapter {N} structure from /books/us-history/pages/{N}-summary and /{N}-key-terms. Record every section URL (/{N}-1-..., /{N}-2-..., etc.) and all official key terms.
2. Pick 1–2 YouTube videos per section (prefer Heimler's History, Crash Course US History, Daily Dose of History, Khan Academy). Capture title, channel, runtime, and full URL.
3. Write three Markdown files in /home/user/workspace/:
   a. Ch{N}_Video_Guide.md — section-by-section. Each section has: linked section title → OpenStax URL, embedded video link(s), then questions formatted as **1a / 1b / 2a / 2b** in bold, each followed by "*Answer:*" and blank lines for handwritten response.
   b. Ch{N}_Vocabulary_Sheet.md — student copy. Every key term listed with blank definition space. Mark the first term with ★ (U+2605) and fill in its definition as an example. Include a Compare & Contrast section (3 prompts), a 7-question matching Self-Check, and one Short-Answer prompt.
   c. Ch{N}_Vocabulary_ANSWER_KEY.md — teacher copy. Full definitions with key phrases **bolded**; Compare & Contrast sample answers; Self-Check answers; Short-Answer scoring guide; Teaching Notes with "Connection back to Ch. {N-1}" and "Connection forward to Ch. {N+1}", key dates to memorize, common confusions, and an ACT/SAT exam tip.
4. Create three Google Docs SEQUENTIALLY (not parallel — parallel calls return null on large docs) via google_docs__pipedream → google_docs-create-document with useMarkdown:true. Exact titles:
   - "Ch {N} — Video Guide & Section Questions (10th Grade US History · OpenStax)"
   - "Ch {N} — Vocabulary Sheet (10th Grade US History · OpenStax)"
   - "Ch {N} — Vocabulary ANSWER KEY — Teacher Copy (10th Grade US History · OpenStax)"
   If a create call returns null, DO NOT retry — call google_docs-find-document with nameSearchTerm set to the title to locate the already-created doc's ID. Extract IDs from the full output file using regex "documentId"\s*:\s*"([^"]+)".
5. Spawn a browser_task with use_local_browser={local:true, question:"Allow Computer to build the Chapter {N} NotebookLM in your admin@checschool.org Drive?"}. Tell it to create a NotebookLM titled exactly "Chapter {N} — US History (10th Grade · OpenStax)" and add 11 sources: 5 OpenStax page URLs (intro + each section), 5 YouTube URLs, and the Answer Key Google Doc via Drive picker. Return the final /notebook/<UUID> URL.
6. Deliver a single final message with the 4 links in a table.
</WORKFLOW>

<FORMAT>
- Every response starts with: Task type: ACADEMICS
- Typographic rules: em dash — (U+2014), middle dot · (U+00B7), star ★ (U+2605). Never substitute hyphen or asterisk.
- Doc titles: "Ch {N} — {Asset} (10th Grade US History · OpenStax)"
- NotebookLM title: "Chapter {N} — US History (10th Grade · OpenStax)"
- Final delivery: 4-row Markdown table (Asset | Purpose | Link), followed by short "What's in Ch. {N}" bullet summary, ending with an offer to continue to Ch. {N+1}.
</FORMAT>

<QUALITY_BAR>
- Verify source count = 11 in NotebookLM before finishing.
- All three Docs open cleanly (no rendering errors).
- Questions use 1a/1b/2a/2b formatting with answer blanks — not a flat numbered list.
- Answer Key Teaching Notes explicitly name the previous and next chapter.
</QUALITY_BAR>

<INPUTS_TO_FILL>
- {N} = chapter number
- {Chapter Title} = exact OpenStax chapter title (e.g., "The Era of Reconstruction, 1865–1877")
</INPUTS_TO_FILL>
```
