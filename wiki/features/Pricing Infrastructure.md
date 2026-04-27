---
title: "Pricing Infrastructure"
type: feature
priority: high
stories: 1
evidence: 8
---

# Pricing Infrastructure

Billing infrastructure that handles usage-based pricing without custom code.

**Stories:** 1 | **Evidence:** 8 quotes across 2 customers

---

## The problem

SaaS companies outgrow flat-rate Stripe subscriptions but can't afford to build usage-based billing from scratch. The transition from "simple subscription" to "metered usage with credits" takes months of engineering. Teams end up maintaining thousands of lines of billing code that nobody wants to touch, or paying $50K+ for enterprise billing platforms.

## Strongest signal

> "We have 14 different billing code paths. Last month we shipped a bug that double-charged 30 customers because one of those paths had a race condition." — [[Customer B]]

> "I want to define my pricing model in a config file and have the system figure out the rest." — [[Customer B]]

## Stories

- [[Manual Billing Doesnt Scale]] — 3 customers, proposed
