# Demo Call — Acme AI and Customer B

**Date:** 2026-03-22
**Participants:** Sam Rivera (Acme AI CEO), Customer B (VP Engineering, Stackform)
**Duration:** 22 minutes

---

**Sam:** Tell me about your billing setup.

**Customer B:** We're a dev tools company. We sell API access and our customers pay based on API calls. The problem is we built our entire billing system on top of Stripe, and it's falling apart. Every time we want to add a new pricing dimension, like charging for compute time in addition to API calls, it takes us two weeks of engineering work because everything is hardcoded.

**Sam:** What specifically breaks?

**Customer B:** Stripe is great for simple subscriptions. But we have customers on annual contracts with custom pricing, customers on usage-based plans, customers on credit systems where they prepay and draw down. Each one is basically a special case in our codebase. We have 14 different billing code paths. Last month we shipped a bug that double-charged 30 customers because one of those paths had a race condition with our usage aggregation job. That was a fun week.

**Sam:** How do you handle the credits model?

**Customer B:** Painfully. Credits are the worst because we have to track balance in real time, handle top-ups, handle what happens when credits expire, handle proration when someone upgrades. We built it all ourselves. It's about 3,000 lines of billing code that three engineers are afraid to touch. Every time someone says "can we add a new plan," I wince because I know it's going to be a two-sprint project.

**Sam:** Have you looked at billing platforms?

**Customer B:** We evaluated Lago and Metronome last year. Lago looked promising but the self-hosted version was a pain and the cloud version didn't support our credit system. Metronome wanted $50K a year minimum, which is more than our entire tooling budget. We looked at building on top of Stripe Billing's metered features but the API is clunky for real-time usage tracking. So we're stuck with our homegrown mess.

**Sam:** What would you need from a solution?

**Customer B:** Something that sits between our app and Stripe. We send it usage events in real time, it handles metering, it handles credits and balances, and it generates the Stripe invoice at the end of the billing cycle. Basically I want to stop thinking about billing infrastructure entirely. I want to define my pricing model in a config file and have the system figure out the rest.

**Sam:** Would you switch if something handled this?

**Customer B:** If it supported credits, custom metrics, and generated Stripe invoices automatically, I'd migrate tomorrow. We spend about 20% of one team's time maintaining billing. That's two engineers who could be building product features instead of debugging why customer 4,721 got charged $0.00 on their invoice.
