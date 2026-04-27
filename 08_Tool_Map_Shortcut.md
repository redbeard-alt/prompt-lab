# /map Shortcut

| Field | Value |
|-------|-------|
| **Title** | Map Shortcut (v2.1) |
| **Status** | Stable |
| **Trigger** | `/map [domain]` |
| **Target AI** | Agentic AI |
| **Model** | Perplexity Pro / Space |
| **Last Updated** | 2026-04-06 |
| **Notes** | Command shortcut for generating taxonomy-builder prompts by domain, with stable CSV naming, collision-safe routing, confidence gating for unknown domains, and self-check enforcement. |

---

## Trigger

When I type:

```
/map [domain]
```

Interpret this as a **command**, not natural language.
Generate a single outcomes-based prompt in a code block for that domain using the exact structure and naming logic below.

---

## Rules

- Use the domain I provide to fill the prompt.
- If the domain is **known** (audit, research, legal, education, history), use the stored phrasing for that domain.
- If the domain is **unknown**:
  - Infer the profession, practitioner label, settings, relationship categories, comparison dimensions, source types, overlap examples, and a reasonable minimum type count.
  - If you must infer **more than 3** of these items, output a `⚠️ WARNING` block **before the code fence** (as regular markdown, not inside it) listing which items were inferred. Invite the user to correct them before using the prompt.
- Default minimum type count is **30+** unless the domain is demonstrably narrow. If you set it below 30, state why in the WARNING block.
- Do not ask me follow-up questions unless the domain is genuinely ambiguous (e.g., could map to multiple professions).
- After generating the prompt, run a **self-check**:
  - All 4 XML sections exist: `<role>`, `<outcome>`, `<constraints>`, `<format>`.
  - The CSV naming rule is present in **both** `<constraints>` and `<format>`.
  - The version stamp comment is present at the top.
  - If any element is missing, regenerate once to fix it.
- Output only the finished prompt in a code block. No extra commentary.

---

## Prompt Template

````xml
<!-- map-shortcut v2.1 | {date} -->

<role>
Act as a {role_title} with 20 years covering {role_domains}.
</role>

<outcome>
Generate a comprehensive {domain} profession knowledge base
containing:

1. A definition of what {entity_plural} are and what they do across
   all settings ({settings}).

2. A comparison table of the relationship-based categories
   ({relationship_categories}) across: {comparison_dimensions}.

3. An exhaustive taxonomy table of EVERY objective-based {domain}
   type that exists — from mainstream ({mainstream_examples})
   through specialized ({specialized_examples}) to emerging
   ({emerging_examples}). Do not limit to a preset list — actively
   search and surface types I may not know about.
   Columns: Type | Primary Objective | Typical Context/Examples.

Audience: A practitioner mapping the full landscape of the
{domain} profession for the first time.
</outcome>

<constraints>
- Cross-reference types across at least 3 independent source lists
  ({source_lists}).
- If a type overlaps significantly with another, note the distinction
  ({overlap_example}).
- If data is unavailable, state: "Data gap."
- You MUST name every taxonomy CSV file using the pattern:
  "{Domain}-Taxonomy-[short-descriptive-label]".
  Do not deviate from this pattern.
</constraints>

<format>
Title the report exactly:
"{Domain} Profession Knowledge Base"

For every structured taxonomy table you export as CSV, title it:
"{Domain}-Taxonomy-[short-descriptive-label]"

Examples:
- "{Domain}-Taxonomy-Core-Types"
- "{Domain}-Taxonomy-Domain-Specific-Types"
- "{Domain}-Taxonomy-Emerging-Types"

Markdown tables for all structured data in the report body.
## headers for sections.
Comprehensive — aim for {min_types} distinct objective-based {domain} types.
</format>

Think deeply about this.
````

---

## Why the Naming Rule Exists

- All taxonomy CSVs share a stable prefix: `{Domain}-Taxonomy-`
- The descriptive suffix makes files human-readable.
- A downstream router can safely normalize outputs into:
  `YYYY-MM-DD--{domain-slug}--taxonomy-{label}.csv`
- If the same file exists, the router can append `--1`, `--2`, etc. without ambiguity.

---

## Stored Domain Presets

### audit
| Variable | Value |
|----------|-------|
| role_title | senior audit and assurance research analyst |
| role_domains | financial, operational, compliance, and emerging audit domains |
| entity_plural | auditors |
| settings | financial, internal, government |
| relationship_categories | internal, external, government/public-sector |
| comparison_dimensions | purpose, independence, scope, reporting lines, and standards |
| mainstream_examples | financial, compliance, operational |
| specialized_examples | grants, construction, ESG |
| emerging_examples | AI/algorithmic bias, smart contract, DEI |
| source_lists | AICPA standards, IIA practice guides, GAO Yellow Book, Big Four methodology publications |
| overlap_example | e.g., compliance audit vs. regulatory inspection |
| min_types | 30+ |

### research
| Variable | Value |
|----------|-------|
| role_title | senior research methodologist |
| role_domains | academic, applied, commercial, and emerging research domains |
| entity_plural | researchers |
| settings | academic, corporate, government, independent |
| relationship_categories | academic/university, industry/corporate, government/public-sector, independent/think tank |
| comparison_dimensions | purpose, funding, independence, publication norms, and typical outputs |
| mainstream_examples | experimental, survey, qualitative |
| specialized_examples | clinical, market, UX |
| emerging_examples | AI/ML research, computational social science, citizen science |
| source_lists | methodology textbooks, professional associations, research design frameworks |
| overlap_example | e.g., action research vs. participatory research |
| min_types | 30+ |

### legal
| Variable | Value |
|----------|-------|
| role_title | senior legal industry analyst |
| role_domains | litigation, transactional, regulatory, and emerging legal practice domains |
| entity_plural | lawyers/legal practitioners |
| settings | private practice, in-house, government, public interest, judiciary |
| relationship_categories | private practice/firm, in-house/corporate counsel, government/public-sector, public interest/nonprofit, judiciary |
| comparison_dimensions | purpose, client relationship, independence, compensation model, and typical outputs |
| mainstream_examples | litigation, corporate/M&A, real estate |
| specialized_examples | admiralty, space law, election law |
| emerging_examples | AI/tech law, cannabis law, climate litigation |
| source_lists | bar association directories, law school curricula, legal industry reports |
| overlap_example | e.g., white-collar defense vs. criminal defense |
| min_types | 40+ |

### education
| Variable | Value |
|----------|-------|
| role_title | senior education profession analyst |
| role_domains | K-12, higher education, corporate training, and emerging instructional domains |
| entity_plural | educators |
| settings | K-12, higher education, corporate/workplace learning, government/policy, community/nonprofit, independent/edtech |
| relationship_categories | K-12 public/private, higher education/university, corporate/workplace L&D, government/policy, community/nonprofit, independent/edtech |
| comparison_dimensions | purpose, learner population, credentialing requirements, funding model, and typical outputs |
| mainstream_examples | curriculum design, special education, ESL/ELL |
| specialized_examples | gifted education, outdoor education, museum education |
| emerging_examples | AI-assisted instruction, learning engineering, micro-credentialing, neuroeducation |
| source_lists | university school-of-education program directories, professional association divisions such as AERA/ISTE/ASCD, credentialing body categories, UNESCO/OECD classification frameworks |
| overlap_example | e.g., instructional design vs. learning engineering, special education vs. inclusive education |
| min_types | 40+ |

### history
| Variable | Value |
|----------|-------|
| role_title | senior historiography and historical profession analyst |
| role_domains | academic, public, applied, and emerging history domains |
| entity_plural | historians |
| settings | academic, public history, government archives, cultural heritage, journalism/documentary, independent |
| relationship_categories | academic/university, public historian/museum/heritage, government/archival/national, journalistic/documentary, independent/freelance |
| comparison_dimensions | purpose, audience served, funding model, methodological norms, and typical outputs |
| mainstream_examples | political, social, economic |
| specialized_examples | maritime, numismatic, oral history |
| emerging_examples | digital humanities, computational history, climate history, history of AI |
| source_lists | AHA fields, university department structures, historical society directories, journal classification schemes |
| overlap_example | e.g., social history vs. cultural history, public history vs. heritage studies |
| min_types | 40+ |

---

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| v2.0 | 2026-04-04 | Added stable CSV prefix naming, multiple taxonomy export support, collision-safe downstream routing. |
| v2.1 | 2026-04-06 | Trigger changed from `map` to `/map`. Added confidence gate for unknown domains (WARNING block). Added self-check rule. WARNING block moved outside code fence. Audit `source_lists` fixed (was echoing placeholder). Default min_types floor set to 30+. Version stamp added to template output. Presets reformatted as tables. Changelog added. |
