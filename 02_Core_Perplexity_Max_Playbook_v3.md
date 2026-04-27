# 02_CORE: THE PERPLEXITY MAX PLAYBOOK v3
> Perplexity Computer prompting, orchestration engine, ecosystem features.
> For templates → 03_Tool | For lookup tables (models, credits) → 04_Tool
> Last updated: March 2026

---

## PART 1: THE OUTCOMES-OVER-PROMPTS PHILOSOPHY

Perplexity Computer shifts AI interaction from **conversation** to **autonomous execution**. You describe a final desired outcome; the system determines the optimal path.

| Dimension | Traditional AI Chatbot | Perplexity Computer |
|-----------|----------------------|---------------------|
| Interaction | Back-and-forth conversation | Complete workflow planning |
| Task Execution | Sequential, manual coordination | Parallel sub-agents |
| Model Selection | Single model per session | 19 models dynamically assigned |
| Environment | Local or stateless | Cloud sandbox with persistence |
| Output | Text responses, suggestions | Finished deliverables, deployments |

**Core principle:** Focus on augmenting your existing tasks. If a Computer workflow saves you 2 hours on a weekly report, it's working. Don't over-engineer.

---

## PART 2: THE ORCHESTRATION ENGINE

Computer doesn't rely on a single model — it intelligently routes tasks across **19+ specialized frontier models**. You never need to pick; the engine assigns automatically based on sub-task type.

### Primary Models

| Model | Strength | Deployed For |
|-------|----------|-------------|
| **Claude Opus 4.6** | Core Reasoning | Workflow planning, deep logical analysis, complex code |
| **Gemini Deep Research** | Research | Broad data gathering, market research, sub-agent creation |
| **ChatGPT 5.2** | Long Context | Broad web searches, creative writing, massive context retention |
| **Grok** | Speed | High-speed tasks, rapid processing, real-time data |
| **Nano Banana** | Visuals | Custom graphics, brand mockups, charts |
| **Veo 3.1** | Video | Video generation, clip extraction, visual storytelling |

> **Note:** These are the 6 primary models among 19+ available. The engine also deploys specialized models for translation, code execution, data parsing, and other sub-tasks. You don't need to know them all — the router handles assignment.

> For the full model selection decision table → **04_Tool**

---

## PART 3: PROMPTING FOR AUTONOMOUS AGENTS

Because Computer breaks your request into sub-tasks and delegates to sub-agents, **micromanaging steps reduces effectiveness**. Follow these 4 principles:

### 1. Describe the Outcome, Not the Steps

Tell Computer what the final result must look like, not how to achieve it.

```
✗ POOR:  Search for AI tools, then compare prices, then make a spreadsheet.
✓ GOOD:  Create a comparison spreadsheet of the top 10 AI productivity tools
         with pricing, features, and user ratings.
```

### 2. Define Scope and Constraints

Provide strict boundaries to prevent scope creep and manage credit usage.

```
- Limit research to sources published after 2024
- Do not exceed 15 pages
- Use only peer-reviewed academic sources
- Credit budget: max 1,000 credits
```

### 3. Request Cross-Referencing

Explicitly ask for comparisons, credibility checks, and deeper insights.

```
- Verify claims with peer-reviewed sources
- Cross-reference all statistics with original data sources
- If data is unavailable, state "Data gap"
```

### 4. Use Role-Based Instructions

Assign a specific perspective to frame the output.

```
Acting as a senior marketing strategist with 15 years experience in B2B SaaS...
```

> **Template for all of the above → 03_Tool Template B**

---

## PART 4: CREDIT ECONOMICS & OPTIMIZATION

Max subscribers receive **10,000 monthly credits** (~$0.02/credit). Complex multi-agent workflows consume more, so active management is required.

> For credit cost estimates by complexity tier → **04_Tool**

### Optimization Strategies

- **Turn off sub-agents for simple tasks** — For straightforward requests that don't need parallel processing, disable sub-agents to save credits
- **Use Pro for basic research** — Reserve Computer strictly for complex, multi-step workflows. Your unlimited Pro searches handle basic queries at zero credit cost
- **Set spending caps** — Navigate to Settings → Credit Management. Set per-task limits (e.g., 500–1,000 credits) to prevent runaway consumption
- **Break big projects down** — Instead of "50-page plan + 100 social posts + website redesign" in one prompt, break into 3 separate focused tasks
- **Check ROI after every task** — Review credit consumption post-completion. Adjust future prompts if a task burned credits disproportionate to its value

### When to Use Computer vs. Pro

| Scenario | Use Computer? | Use Pro? |
|----------|:---:|:---:|
| Basic web search | | ✓ |
| Compare 3 articles | | ✓ |
| Summarize 1 PDF | | ✓ |
| Draft a single email | | ✓ |
| Build live web app | ✓ | |
| 50-page report with citations | ✓ | |
| Cross-reference 10 studies + visualization | ✓ | |
| Deploy to Google Drive | ✓ | |
| Multi-format deliverable package | ✓ | |

**Rule of thumb:** If a single model can handle it in one turn with no tools → use Pro. If it needs parallel research, code execution, file generation, or connectors → use Computer.

---

## PART 5: ECOSYSTEM FEATURES

### Spaces

Organize projects into separate workspaces:
- Set **custom AI instructions** per Space (behavior, tone, constraints)
- Upload **project-specific files** (brand guides, past reports, reference docs)
- Invite **team members** to collaborate
- Each Space maintains its own conversation history and context

**Power combo:** Create a Space → upload reference files → set custom instructions → invoke Computer with outcome-based prompt. The engine uses your Space files as grounding context.

### App Connectors

Computer integrates with **100+ services** (Google Drive, Slack, Notion, GitHub) to pull data or push finished deliverables directly.

```
Deliver results to [DESTINATION] as [FORMAT].
Push final report to my connected Google Drive folder as PDF.
```

Connectors eliminate the "download → rename → upload" friction. Always specify the delivery target in your prompt when you want direct integration.

### Model Council

For high-stakes verification, run a query across **3 different AI models simultaneously**. The system outputs a structured comparison table showing where models agree and disagree.

**Use cases:**
- Fact-checking critical decisions
- Validating research findings
- Testing prompt variations across models

### Comet Browser

An AI-first browser with voice command control:
- "Summarize this page"
- "Open the first result"
- Automate site actions (clicking, waiting, extracting)

Useful for hands-free research sessions and rapid web interaction.

---

## PART 6: PERSONAL COMPUTER (Local + Cloud Hybrid)

As of March 2026, Max subscribers can access **Personal Computer** — an always-on, proactive automation agent running 24/7 on a dedicated Mac mini.

### How It Differs from Cloud Computer

| Dimension | Cloud Computer | Personal Computer |
|-----------|---------------|-------------------|
| Activation | Manual prompt | Trigger-based (proactive) |
| File access | Uploaded files only | Full local file system + local apps |
| Persistence | Session-based | Always-on, 24/7 |
| Execution | Cloud sandbox | Local Mac mini |

### Key Capabilities

- **Local Access** — Full access to local file system and installed applications (unlike cloud Computer)
- **Proactive Automation** — Executes workflows based on triggers, not manual prompts. Example: *"When an invoice PDF arrives in email, extract data and update the accounting spreadsheet."*
- **Security Controls** — Kill switch for immediate stop; requires explicit approval before sensitive actions; operates within strictly defined scope

### When to Use Personal Computer vs. Cloud Computer

| Use Case | Personal Computer | Cloud Computer |
|----------|:-:|:-:|
| Scheduled/triggered workflows | ✓ | |
| Local file manipulation | ✓ | |
| Local app automation | ✓ | |
| One-off research projects | | ✓ |
| Multi-model deliverables | | ✓ |
| Team collaboration via Spaces | | ✓ |

---

## PART 7: BEST PRACTICES

### DO

- Describe final outcomes, not steps
- Define strict scope and constraints
- Use Computer for multi-step, multi-model workflows
- Set per-task credit limits
- Break large projects into focused tasks
- Leverage Spaces for project organization
- Use App Connectors for direct integrations
- Request cross-referencing and verification
- Check credit consumption after every task

### DON'T

- Micromanage individual steps
- Use Computer for simple tasks (use Pro)
- Combine unrelated deliverables in one prompt
- Skip scope constraints (leads to credit waste)
- Ignore credit consumption patterns
- Use conversational back-and-forth (describe the outcome once)
- Don't overload AI with giant custom-instruction walls. Set light guardrails, then control verbosity and structure per task.

---

## EXAMPLE WORKFLOW: SPACES + COMPUTER

```
1. Create a Space for "Q1 Marketing Campaign"
2. Upload: brand guidelines, past campaign reports
3. Set Custom Instructions: "Act as CMO. Verify all claims.
   Format for executive audience."
4. Invoke Computer:
   "Generate a complete Q1 marketing campaign package including
   landing page wireframes, 20 social posts, email sequences,
   and performance dashboard. Deliver to my Google Drive as
   organized folders."
5. Computer orchestrates:
   Nano Banana → visuals | ChatGPT → copy | Claude → strategy | Gemini → research
6. Result: Complete deliverable pushed to Drive in one workflow.
```

> **For the fill-in template → 03_Tool Template B**
> **For credit estimates → 04_Tool**
