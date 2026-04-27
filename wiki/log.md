# Log

## [2026-04-27] ingest | David Garnitz call

**Changes:**
- Created [[David Garnitz]] customer page — 7 quotes extracted
- Updated [[Runaway AI Costs Without Guardrails]] — added 4 quotes from David, evidence count 4 → 5 customers
- Updated [[Cost Intelligence]] — evidence count 14 → 19 quotes across 10 → 11 customers
- Updated index with new customer entry

**Why:** David is a friend/peer (AI infra engineer at a ~40-person startup), not a prospect. But his signal is strong: his company just burned $200K on an unguarded API cost bug in production. Cloud providers don't implement hard limits by default (AWS literally won't). His team of 40 devs tunes out alerts. He suggested a wrapper/proxy that blocks API calls at threshold — maps directly to the guardrails story. He also said he'd install a free CLI/package for cost visibility even if he wouldn't pay on day one — GTM signal for open-source/freemium entry.

**Held back:**
- David's comments about Langfuse competition and "crowded space" are market intelligence but don't map to a specific story. Captured on customer page only.
- "Not a startup problem... more of a serious risk at growing companies" — market positioning signal, not a story. On customer page.

## [2026-03-15] ingest | Example transcript — Customer A (NovaTech)

**Changes:**
- Created [[Customer A]] customer page — 8 quotes extracted
- Updated index with new page

**Why:** First example ingestion. AI writing assistant struggling with per-customer token cost visibility and flat-rate pricing that doesn't match usage.

## [2026-03-22] ingest | Example transcript — Customer B (Stackform)

**Changes:**
- Created [[Customer B]] customer page — 8 quotes extracted
- Updated index with new page

**Why:** Dev tools company with 14 billing code paths and credit system complexity. Strong signal on billing infrastructure pain.

## [2026-03-29] ingest | Example transcript — Customer C (Peakflow)

**Changes:**
- Created [[Customer C]] customer page — 7 quotes extracted
- Updated index with new page

**Why:** AI analytics platform wanting outcome-based pricing but can't simulate changes or meter custom metrics.

## [2026-03-29] synthesize | Story and feature synthesis

**Changes:**
- Created story [[No Per-Customer Margin Visibility]] — linked [[Customer A]], [[Customer C]]
- Created story [[Manual Billing Doesnt Scale]] — linked [[Customer A]], [[Customer B]]
- Created feature [[Cost Intelligence]] — 1 story, 15 quotes
- Created feature [[Pricing Infrastructure]] — 1 story, 8 quotes
- Updated index with all new pages

**Why:** Grouped 23 quotes across 3 customers into recurring themes. Two clear feature areas emerged: cost visibility and billing infrastructure.
