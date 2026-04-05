# PROMPT LAB: TROUBLESHOOTING & MULTI-TURN STRATEGY
> Prompt debugging, failure recovery, and conversation management.
> Last updated: March 2026

---

## PART 1: PROMPT DIAGNOSTIC TREE

When output is wrong, walk this tree top-to-bottom. Fix the FIRST failure point.

```
Output failed expectations
│
├─ 1. TASK CLARITY
│   Is the task verb specific? Is the end goal unambiguous?
│   ✗ → Rewrite with precise action verb + measurable outcome
│
├─ 2. CONTEXT COMPLETENESS
│   Did you answer all 3 context questions? (Role, Success, Constraints)
│   ✗ → Add missing context. Run 3-Question Context Filter (→ 04_Tool)
│
├─ 3. MODEL FIT
│   Is this the right model for the task type?
│   ✗ → Check Model Selection table (→ 04_Tool). Switch models.
│
├─ 4. PARADIGM FIT
│   Standard LLM task getting agentic treatment, or vice versa?
│   ✗ → Re-route via Decision Tree (→ 00_Index)
│
├─ 5. FORMAT SPEC
│   Did you specify exact output structure?
│   ✗ → Add explicit format tags. Be surgical: columns, sections, length.
│
├─ 6. EXEMPLAR GAP
│   Is the AI guessing at style/structure without a reference?
│   ✗ → Attach an example or specify a framework (STAR, MECE, etc.)
│
├─ 7. CONTEXT WINDOW OVERFLOW
│   Is the conversation too long? Is the model forgetting earlier context?
│   ✗ → See Part 3: Multi-Turn Strategy
│
└─ 8. MODEL REFUSAL / SAFETY FILTER
    Did the model refuse or give a watered-down response?
    ✗ → See Part 4: Handling Refusals
```

---

## PART 2: COMMON FAILURE PATTERNS

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Output is generic / surface-level | Missing context or exemplars | Add specifics: numbers, names, constraints, attach examples |
| Output is wrong format | No format tag or vague spec | Use explicit `<format>` with exact structure |
| Output contradicts itself | Task is compound / ambiguous | Split into separate focused prompts |
| Output is too long | No verbosity control | Append verbosity phrase (→ 04_Tool) |
| Output hallucinated facts | No cross-reference constraint | Add: "Cite sources. If uncertain, state 'unverified'" |
| Agentic task burned credits, weak result | Over-specified steps | Strip process instructions. Describe outcome only. |
| Model ignores part of the prompt | Prompt too long / buried instructions | Move critical instructions to TOP. Use XML tags for structure. |
| Second response contradicts first | Context window drift | Summarize key decisions so far, restate constraints |

---

## PART 3: MULTI-TURN CONVERSATION STRATEGY

### When to Continue vs. Start Fresh

| Scenario | Action |
|----------|--------|
| Refining tone/style of existing output | Continue |
| Adding a section to existing work | Continue |
| Conversation > 8 back-and-forth turns | Consider fresh start |
| Changing topic or task entirely | Fresh start |
| Model starts repeating or contradicting itself | Fresh start with summary |
| Output quality degrading | Fresh start; reverse-engineer best output first |

### Context Window Management

1. **Summarize before continuing** — After 4-5 turns: "Before we continue, here's what we've established: [key decisions, constraints, and current draft state]"
2. **Progressive disclosure** — Don't front-load everything. Give context → get draft → then add constraints/exemplars
3. **Pin critical constraints** — Restate non-negotiable requirements in EVERY follow-up prompt, not just the first
4. **Use Prompt Reversal as a checkpoint** — If conversation has been productive, reverse-engineer before continuing: captures the best prompt state

### Iterative Refinement Ladder

```
Level 1: Constraint tightening
  "Good start. Now add [specific constraint] and remove [specific element]."

Level 2: Targeted rewrite
  "Section 3 is weak. Rewrite it to [specific improvement criteria]."

Level 3: Perspective shift
  "Now review this as [new persona]. What would you change?"

Level 4: Red Team + Fix cycle
  "Attack the weakest points. Then rewrite those sections."

Level 5: Prompt Reversal
  "Reverse-engineer this conversation into a single prompt."
```

---

## PART 4: HANDLING REFUSALS

When the model declines or gives a hedged response:

1. **Legitimate safety boundary** → Respect it. Rephrase the task to avoid the sensitive area while still achieving your goal.
2. **False positive** → Reframe without trigger words. Add professional context: "I am a [role] doing [legitimate task] for [legitimate purpose]."
3. **Overly cautious output** → Add: "Be direct. Skip disclaimers. I need actionable specifics, not caveats."
4. **"I can't access that"** → Check if it's a capability limitation (not a refusal). Switch tools or models.

> **NEVER** attempt jailbreaks or injection attacks. They waste time, produce unreliable output, and may flag your account.

---

## PART 5: QUICK DIAGNOSTIC CHECKLIST

Before hitting send on any important prompt, verify:

- [ ] Task has a specific action verb and measurable end goal
- [ ] Context answers: Who am I? What does success look like? What are my constraints?
- [ ] Format is explicitly specified (not left to AI's discretion)
- [ ] Right paradigm chosen (Standard LLM vs. Agentic)
- [ ] Right model chosen for task type
- [ ] Verbosity control phrase appended
- [ ] Router nudge appended (if complex/high-stakes)
- [ ] Exemplar provided (if style/structure matters)
