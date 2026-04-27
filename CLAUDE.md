# BuildNext — Schema

BuildNext is an evidence-grounded product knowledge base. Raw customer signal goes in, structured user stories come out. An LLM maintains the wiki — the human curates.

## Structure

```
raw/              # Input: call transcripts, notes, tickets (immutable)
wiki/             # Output: LLM-maintained markdown (Obsidian vault)
  customers/      # Entity pages — one per customer, extracted quotes
  stories/        # Synthesized user stories with acceptance criteria
  features/       # Story groupings by product area
  index.md        # Master catalog of all pages
  log.md          # Chronological operation record
CLAUDE.md         # This file — schema and rules
config.md         # Internal speakers, evidence tags, project settings
```

## Three layers

- **raw/** — Source material. Transcripts, notes, tickets pasted as markdown. Never modified after creation. The LLM reads from here but never writes.
- **wiki/** — LLM-generated output. Obsidian vault with YAML frontmatter, `[[wikilinks]]`, and `#tags`. Updated on every ingest.
- **CLAUDE.md** — Rules for how the LLM reads, writes, and maintains the system.
- **config.md** — Project-specific settings: internal speakers to exclude, evidence tags, and preferences.

## Obsidian conventions

All wiki pages use these Obsidian features:

- **YAML frontmatter** — every page has Properties (title, type, tags, etc.) rendered in Obsidian's Properties panel
- **`[[wikilinks]]`** — all cross-references use Obsidian-style links
- **`#tags`** — evidence tags use Obsidian's native `#tag` format (not backtick code). Tags are clickable, appear in the tag pane, and color the graph
- **Callouts** — use `> [!note]` for conflicts, `> [!warning]` for paraphrased/non-verbatim sources
- **Frontmatter tags array** — aggregate tags also listed in YAML `tags:` field for Properties-based filtering

## Page types

### Customer pages (`wiki/customers/`)

One page per customer or conversation. Contains extracted quotes with speaker attribution and evidence tags.

Format:
```markdown
---
title: "Customer Name"
type: customer
company: "Company Name"
dates: "YYYY-MM-DD, YYYY-MM-DD"
evidence: N
tags: [pain-point, buying-signal, workflow]
---

# Customer Name

- "exact quote from the customer" — Speaker #qualitative #pain-point
- "another exact quote" — Speaker #buying-signal
```

Rules:
- Use EXACT quotes, not summaries
- Minimum 15 words per quote
- **Speaker identification**: read the transcript to figure out who said what. Attribute each quote to the correct speaker by name.
- **Internal speaker filtering**: read `config.md` for the list of internal team members. Skip their quotes — only extract from external speakers (customers, prospects, partners).
- **Tagging**: tag each quote using Obsidian `#tags` from the evidence tags defined in `config.md` (e.g. `#qualitative`, `#pain-point`, `#feature-request`, `#buying-signal`). A quote can have multiple tags. Also list unique tags in frontmatter `tags:` array.
- **Request classification**: classify each quote with one request type tag:
  - `#req/feature-request` — new capability that doesn't exist
  - `#req/enhancement` — improve something that already works
  - `#req/bug` — something broken
  - `#req/ux-friction` — works but painful to use
  - `#req/internal-request` — internal team needs tooling
  - `#req/integration` — connect to external system
  - `#req/compliance` — security, legal, regulatory requirement
  - `#req/churn-signal` — customer explicitly tied this to renewal/cancellation
  Request type goes alongside evidence tags on the same line (e.g. `#pain-point #req/feature-request`).
- Update existing customer pages when new transcripts arrive — append, don't overwrite
- If source is paraphrased notes (not verbatim transcript), add `> [!warning]` callout noting this
- **Source tracking**: note the source type in the quote attribution when it's not a call transcript (e.g. Slack, support ticket, email). Default assumption is call transcript.

## Data sources

Evidence can come from multiple sources beyond call transcripts:

- **Call transcripts** (Airtable Meetings table) — primary source, verbatim quotes
- **Slack messages** — customer DMs, shared channels, support threads
- **Support tickets** — bug reports, feature requests filed by customers
- **Email** — inbound customer emails with signal
- **Notes** — internal notes from meetings (mark as paraphrased if not verbatim)

When ingesting from non-transcript sources, tag the source type on the quote:
```
- "quote from slack" — [[Customer Name]] #pain-point (via Slack)
```

### Story pages (`wiki/stories/`)

Synthesized user stories grounded in evidence. Every story must trace back to customer quotes.

Format:
```markdown
---
title: "Story Title"
type: story
status: proposed | accepted | shipped
story-type: feature-request | enhancement | bug | ux-friction | internal-request | integration | compliance | churn-signal
priority: high | medium | low
evidence: N
feature: "[[Feature Name]]"
---

# Story Title

**Status:** proposed
**Type:** new_feature
**Evidence:** N customers

## User Story

> As a [persona] I want [action] so that [outcome]

## Acceptance Criteria

- [ ] Criterion 1
- [ ] Criterion 2

## Evidence

- "supporting quote" — [[Customer Name]] #pain-point #workflow
- "another quote" — [[Customer Name]] #buying-signal
```

Rules:
- No evidence, no story. Never generate stories from nothing.
- Acceptance criteria must be testable.
- **Inline attribution**: every quote has `[[wikilink]]` to its customer on the same line — no grouping under customer headers.
- Tags use `#tag` format on each quote.

### Feature pages (`wiki/features/`)

Group related stories by product area. Lead with the problem, not the story list.

Format:
```markdown
---
title: "Feature Area Name"
type: feature
priority: high | medium | low
stories: N
evidence: N
---

# Feature Area Name

One-line summary of the core problem.

**Stories:** N | **Evidence:** N quotes across N customers

---

## The problem

2-3 paragraphs explaining what's broken, with specific customer references.

## Strongest signal

> "best quote" — [[Customer Name]]

> "second best quote" — [[Customer Name]]

## Stories

- [[Story Title]] — N customers, status
- [[Story Title]] — N customers, status
```

## Cross-referencing

Use `[[wikilinks]]` to link between pages. When creating or updating a page:
- Link to all relevant customer and story pages.
- If referencing something without a page, note it as `See also: [[Page Name]] (not yet created)`.
- Filenames: use the entity/story name directly (e.g., `customers/Acme Corp.md`).

## Workflows

### Ingest

When given a transcript or raw source:

1. Save the raw text to `raw/` with a descriptive filename.
2. Extract quotes — filter out internal speakers, keep exact words, tag with `#tags`.
3. Create or update the customer page in `wiki/customers/` with YAML frontmatter.
4. Check if quotes map to existing stories or suggest new ones.
5. Update `wiki/index.md` with new/modified pages.
6. Append to `wiki/log.md` with a detailed changelog (see Log format below).

### Synthesize

When asked to generate stories:

1. Read all customer pages for recurring themes.
2. Group related quotes across customers.
3. Generate user stories with acceptance criteria grounded in the evidence.
4. Create story pages in `wiki/stories/` with inline `[[wikilink]]` attribution on every quote.
5. Group stories into features in `wiki/features/` with problem-first format.
6. Update index and log.

### Lint

When asked to health-check:

1. **Orphan quotes** — evidence not linked to any story.
2. **Weak stories** — only one customer's evidence.
3. **Missing links** — wikilinks pointing to nonexistent pages.
4. **Stale pages** — customers with no recent evidence.
5. **Frontmatter gaps** — pages missing required YAML properties.
6. Append findings to `wiki/log.md`.

### Query

When asked a question about the evidence:

1. Read `wiki/index.md` to find relevant pages.
2. Read relevant pages and synthesize an answer.
3. Cite sources using wikilinks.

## Log format

`wiki/log.md` is append-only and chronological. Every entry must be specific and auditable.

```markdown
## [YYYY-MM-DD] operation | Brief Title

**Changes:**
- Added 3 quotes to [[Customer Name]] from call 2026-04-20
- Created story [[Story Title]] — linked [[Customer A]], [[Customer B]], [[Customer C]]
- Updated [[Feature Name]] — new story added, evidence count 6 → 9
- Changed [[Story Title]] status from proposed → accepted (reason: 3rd customer confirmed the pain)

**Why:** New transcript from [[Customer Name]] contained strong buying signals and pain points around X. Quotes mapped to existing story [[Y]] and also warranted a new story [[Z]] because no existing story covered theme W.

**Held back:**
- New quote from [[Customer X]] suggests feature Y is low priority. Conflicts with human edit that moved [[Story Z]] to accepted. No change made — flagged for review on the story page with `> [!note]` callout.
```

Operations: `ingest`, `synthesize`, `query`, `lint`, `update`, `create`, `curate` (human edit detected).

Rules:
- **Name every page** changed, created, or suppressed
- **Explain why** changes were made — what evidence triggered the change
- **Log non-actions** — if evidence was held back due to human edit conflicts, say what and why
- Never log vague summaries like "ingested transcript"

## Human edits

The human may edit any wiki page at any time. When the agent encounters human edits:

1. **Never overwrite.** If a page has been manually edited, preserve those changes. The human's version wins.
2. **Detect edits.** Before updating a page, read its current state. If content differs from what the agent last wrote (restructured stories, renamed features, deleted quotes, added notes), treat it as intentional curation.
3. **Log it.** Append to `wiki/log.md`: `## [date] curate | Page Name` with a note of what the human changed.
   - Also log **suppressed changes**: if new evidence would conflict with a human edit, log what was held back and why so the human can review it.
4. **Learn from it.** Human edits are implicit feedback on how the agent should work:
   - Deleted a story? The agent was wrong to create it. Don't regenerate it.
   - Moved a story to a different feature? That's the correct grouping going forward.
   - Reworded acceptance criteria? Use that style for future stories.
   - Added a note or context? Preserve it in all future updates.
5. **Surface conflicts.** If new evidence contradicts a human edit, don't silently override. Flag it: add a `> [!note] New evidence may affect this` callout and let the human decide.

The wiki gets smarter over time because every human edit teaches the agent what "good" looks like for this specific project.

## Principles

- **No evidence, no story.** Everything traces back to what customers said.
- **The human curates; the LLM maintains.** You upload, the agent organizes.
- **Human edits are sacred.** Never overwrite manual changes. Learn from them.
- **Compound, don't repeat.** Every ingest makes the wiki richer.
- **Cite everything.** Claims trace back to raw sources.
- **Prefer updating to creating.** Check for existing pages first.
- **Use Obsidian natively.** Frontmatter, `#tags`, `[[wikilinks]]`, callouts — not custom formatting.

## Skill routing

When the user's request matches an available skill, invoke it via the Skill tool. The
skill has multi-step workflows, checklists, and quality gates that produce better
results than an ad-hoc answer. When in doubt, invoke the skill. A false positive is
cheaper than a false negative.

Key routing rules:
- Product ideas, "is this worth building", brainstorming → invoke /office-hours
- Strategy, scope, "think bigger", "what should we build" → invoke /plan-ceo-review
- Architecture, "does this design make sense" → invoke /plan-eng-review
- Design system, brand, "how should this look" → invoke /design-consultation
- Design review of a plan → invoke /plan-design-review
- Developer experience of a plan → invoke /plan-devex-review
- "Review everything", full review pipeline → invoke /autoplan
- Bugs, errors, "why is this broken", "this doesn't work" → invoke /investigate
- Test the site, find bugs, "does this work" → invoke /qa (or /qa-only for report only)
- Code review, check the diff, "look at my changes" → invoke /review
- Visual polish, design audit, "this looks off" → invoke /design-review
- Developer experience audit, try onboarding → invoke /devex-review
- Ship, deploy, create a PR, "send it" → invoke /ship
- Merge + deploy + verify → invoke /land-and-deploy
- Configure deployment → invoke /setup-deploy
- Post-deploy monitoring → invoke /canary
- Update docs after shipping → invoke /document-release
- Weekly retro, "how'd we do" → invoke /retro
- Second opinion, codex review → invoke /codex
- Safety mode, careful mode, lock it down → invoke /careful or /guard
- Restrict edits to a directory → invoke /freeze or /unfreeze
- Upgrade gstack → invoke /gstack-upgrade
- Save progress, "save my work" → invoke /context-save
- Resume, restore, "where was I" → invoke /context-restore
- Security audit, OWASP, "is this secure" → invoke /cso
- Make a PDF, document, publication → invoke /make-pdf
- Launch real browser for QA → invoke /open-gstack-browser
- Import cookies for authenticated testing → invoke /setup-browser-cookies
- Performance regression, page speed, benchmarks → invoke /benchmark
- Review what gstack has learned → invoke /learn
- Tune question sensitivity → invoke /plan-tune
- Code quality dashboard → invoke /health
