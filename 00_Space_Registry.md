# Space Registry
## Cross-Space Path Contract v1

> Canonical registry for Perplexity Spaces stored under `$PXROOT`.
> Source of truth lives in `_shared/` and is synced into participating Spaces.

---

## Base Path

```bash
export PXROOT="/Users/bryanjhein/Library/CloudStorage/Dropbox-Privaterelay/Bryan Hein/Perplexity"
```

All Space folders live directly under `$PXROOT` and match the exact Perplexity Space name.

---

## Space Table

| Space Name | Folder Path |
|---|---|
| CHEC Independent School | `$PXROOT/CHEC Independent School` |
| CHEC Student | `$PXROOT/CHEC Student` |
| Hein Institute | `$PXROOT/Hein Institute` |
| Individual Profile Builder | `$PXROOT/Individual Profile Builder` |
| Org Profiler Space | `$PXROOT/Org Profiler Space` |
| Parenting | `$PXROOT/Parenting` |
| Persona Foundry | `$PXROOT/Persona Foundry` |
| PromptLab | `$PXROOT/PromptLab` |
| Terminal Lab | `$PXROOT/Terminal Lab` |

---

## Rules

- Folder names must match the exact Perplexity Space name.
- Cross-Space patches must reference target Spaces by this exact name.
- If a Space is renamed in Perplexity, update this registry first, then sync.
- Shared commands that generate file paths must resolve Space folders through this registry, not by inference.

---

## Version History

| Version | Date | Changes |
|---|---|---|
| v1 | 2026-04-14 | Initial registry with 9 Spaces |
