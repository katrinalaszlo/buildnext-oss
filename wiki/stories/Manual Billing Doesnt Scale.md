---
title: "Manual Billing Doesn't Scale"
type: story
status: proposed
story-type: feature-request
priority: high
evidence: 3
feature: "[[Pricing Infrastructure]]"
---

# Manual Billing Doesn't Scale

**Status:** proposed
**Type:** feature-request
**Evidence:** 3 customers

## User Story

> As a developer building a SaaS product I want billing infrastructure that handles usage-based pricing, credits, and custom metrics so that I can stop maintaining thousands of lines of billing code

## Acceptance Criteria

- [ ] Usage event ingestion in real time
- [ ] Credit system with balance tracking, top-ups, and expiry
- [ ] Custom metric support (not just API calls — compute time, insights, tokens)
- [ ] Automatic Stripe invoice generation at end of billing cycle
- [ ] Pricing model defined in config, not code

## Evidence

- "We have 14 different billing code paths. Last month we shipped a bug that double-charged 30 customers." — [[Customer B]] #pain-point
- "We've talked about usage-based pricing for six months. Our engineers quoted it at three months of work." — [[Customer A]] #pain-point
- "Credits are the worst. It's about 3,000 lines of billing code that three engineers are afraid to touch." — [[Customer B]] #pain-point
