---
title: "Customer B"
type: customer
company: "Stackform"
dates: "2026-03-22"
evidence: 8
tags: [pain-point, workflow, buying-signal, feature-request, quantitative]
---

# Customer B

- "Every time we want to add a new pricing dimension, like charging for compute time in addition to API calls, it takes us two weeks of engineering work because everything is hardcoded." — Customer B #pain-point #workflow #req/ux-friction
- "We have 14 different billing code paths. Last month we shipped a bug that double-charged 30 customers because one of those paths had a race condition with our usage aggregation job." — Customer B #pain-point #quantitative #req/bug
- "Credits are the worst because we have to track balance in real time, handle top-ups, handle what happens when credits expire, handle proration when someone upgrades. It's about 3,000 lines of billing code that three engineers are afraid to touch." — Customer B #pain-point #workflow #req/feature-request
- "We evaluated Lago and Metronome last year. Lago's self-hosted version was a pain. Metronome wanted $50K a year minimum, which is more than our entire tooling budget." — Customer B #pain-point #quantitative #req/feature-request
- "I want to define my pricing model in a config file and have the system figure out the rest." — Customer B #feature-request #qualitative #req/feature-request
- "We spend about 20% of one team's time maintaining billing. That's two engineers who could be building product features instead of debugging why customer 4,721 got charged $0.00 on their invoice." — Customer B #quantitative #pain-point #req/ux-friction
- "Something that sits between our app and Stripe. We send it usage events in real time, it handles metering, it handles credits and balances, and it generates the Stripe invoice at the end of the billing cycle." — Customer B #feature-request #workflow #req/feature-request
- "If it supported credits, custom metrics, and generated Stripe invoices automatically, I'd migrate tomorrow." — Customer B #buying-signal #feature-request #req/feature-request
