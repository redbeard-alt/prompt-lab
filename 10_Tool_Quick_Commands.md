# Quick Commands — PromptLab Only
## PromptLab-Specific Quick Commands v1

> These commands are specific to the PromptLab Space. For universal commands (HAND OFF, RED TEAM, FIX), see `00_Quick_Commands_Universal.md`.

---

## Command Registry

| Command | Arguments | What It Does |
|---|---|---|
| `REVERSE-ENGINEER` | none | Produces a single one-shot prompt that recreates the final output |
| `SAVE` | none | Stores the last reversed prompt in 05_Store by USE CASE |
| `AMPLIFY` | none | Spins the last output into other formats |
| `/map` | `domain` (required) | Generates an outcomes-based taxonomy prompt for the given domain |

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

**Behavior:** See 08_Tool_Map_Shortcut.md for full implementation. Generates an outcomes-based taxonomy-builder prompt for the given domain.

---

## Version History

| Version | Date | Changes |
|---|---|---|
| v1 | 2026-04-14 | Split from quickcommands-2.md. PromptLab-only commands: REVERSE-ENGINEER, SAVE, AMPLIFY, /map |
