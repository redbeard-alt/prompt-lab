# Homeschool Chapter Trio Builder

**Use case:** Homeschool / Curriculum Build — produces a 4-asset per-chapter bundle for the OpenStax U.S. History 10th-grade course.

## Files

| File | Purpose |
|---|---|
| `v1-original.md` | Original prompt as reverse-engineered from the live session. Kept for history. Do not use. |
| `red-team-notes.md` | 20 failure modes catalogued during adversarial review. |
| `v2-fixed.md` | Current production prompt. All 20 issues resolved. See its `<CHANGE_LOG>` for traceability. |

## What it produces

For any chapter N (1–29):
1. Video Guide + Section Questions (Google Doc)
2. Vocabulary Sheet — student copy (Google Doc)
3. Vocabulary Answer Key — teacher copy (Google Doc)
4. NotebookLM with all chapter sources loaded

## How to use

Paste `v2-fixed.md` into Perplexity Computer. Fill the two `<INPUTS>` values (`{N}` and optionally `{Chapter Title}`). The agent handles OpenStax fetching, video verification, Google Docs creation, and NotebookLM build — with budget ceilings and partial-delivery rules.

## Tested on

- Ch. 15 (*The Civil War, 1860–1865*) — v1 succeeded; surfaced most failure modes that v2 now handles.
- Ch. 14 (*Troubled Times: the Tumultuous 1850s*) — v1 succeeded but created duplicate Answer Key; addressed in v2 via timestamp filtering.
