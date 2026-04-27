---
title: "Pricing Infrastructure"
type: feature
priority: high
stories: 3
---

# Pricing Infrastructure

Stripe handles payments. Everything between the payment and the product — entitlements,  metering,  pricing logic — companies build by hand or don't build at all.

**Stories:** 3 | **Evidence:** 18 quotes across 11 customers

---

## The problem

Three flavors of the same gap:

**Manual billing that breaks at scale.** Moe Amaya creates Stripe subscriptions by hand and flips autopay after payment. Chris Price manually adds credits. These workarounds hold for 5-10 customers. They collapse at 50.

**Can't bill for outcomes.** Corey Engel needs to charge per document generated and data ingested — metrics Stripe doesn't model. Joe Siracusa wants pricing triggered by customer milestones like funding rounds. Rob Enslow charges cost-plus on AI credits but wants to move to per-meeting-booked.

**Build vs buy stalemate.** Rob Enslow says he can build anything in an hour with Claude. Jerry O'Shea's company rejected Paid AI after a $50K pro-serve proposal. Colby Hill doesn't feel urgency. The bar: simpler than DIY,  cheaper than enterprise vendors.

## Strongest signal

> "right now we're very very jerryrigged. Basically I just send someone a subscription like I go into Stripe and I create a subscription object and I just send them the payment link." — [[Moe Amaya]]

> "I have to create custom metrics for how I want to bill third party consultancies based on what they're producing,  how they're producing it,  and what decisions are being made. Haven't been able to." — [[Corey Engel]]

## Stories

- [[Manual Stripe Workflows Don't Scale]] — 6 customers,  high
- [[Can't Bill for Custom Outcome Metrics]] — 4 customers,  medium
- [[Build vs Buy Tension for Billing]] — 5 customers,  medium
