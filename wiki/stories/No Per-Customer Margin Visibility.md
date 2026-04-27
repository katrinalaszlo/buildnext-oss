---
title: "No Per-Customer Margin Visibility"
type: story
status: proposed
story-type: feature-request
priority: high
evidence: 3
feature: "[[Cost Intelligence]]"
---

# No Per-Customer Margin Visibility

**Status:** proposed
**Type:** feature-request
**Evidence:** 3 customers

## User Story

> As a SaaS founder I want to see revenue minus cost per customer so that I can identify unprofitable accounts and restructure pricing based on data instead of gut feelings

## Acceptance Criteria

- [ ] Per-customer view showing revenue, cost, and margin
- [ ] Cost tracking from LLM providers attributed to each customer
- [ ] Alerting when a customer's margin drops below a threshold
- [ ] No manual data entry — pull from Stripe + usage APIs automatically

## Evidence

- "We have no idea what our actual margin is per customer. We just look at the aggregate Stripe revenue and subtract our OpenAI bill and hope the number is positive." — [[Customer A]] #pain-point
- "Our top-tier customers get 100x the value of our smallest customers but only pay 3x more. And I can't prove that to my board." — [[Customer C]] #pain-point
- "I think maybe 10% of our customers are unprofitable, but I literally cannot prove it." — [[Customer A]] #pain-point
