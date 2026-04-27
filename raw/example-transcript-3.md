# Demo Call — Acme AI and Customer C

**Date:** 2026-03-29
**Participants:** Sam Rivera (Acme AI CEO), Customer C (CEO, Peakflow)
**Duration:** 20 minutes

---

**Sam:** What's your pricing model?

**Customer C:** We're an AI analytics platform. We charge based on data volume processed. The problem is I want to move to outcome-based pricing — charge customers based on the value we deliver, like insights generated or anomalies detected — but I have no way to meter that. Our billing system only understands rows processed.

**Sam:** What's driving the change?

**Customer C:** Customers keep asking. Our biggest customer told me "I don't care how many rows you process, I care how many actionable insights you surface." They're right. But right now I'd have to build a custom metering system to track insights-per-customer, wire it into our billing, and figure out the right price per insight. I have no idea how to price something that's never been priced before.

**Sam:** How do you figure out what to charge?

**Customer C:** I can't. That's the problem. If I want to model "what happens to revenue if we charge $2 per insight instead of $0.50 per thousand rows," I have to build a spreadsheet and guess. There's no tool that lets me simulate pricing changes against real usage data before rolling them out. So I'm stuck with the pricing model we launched with, even though I know it's wrong.

**Sam:** What's the cost of staying on the current model?

**Customer C:** We're leaving money on the table. Our top-tier customers get 100x the value of our smallest customers but only pay 3x more. And I can't prove that to my board because I can't show per-customer unit economics. My CFO asks me every month what our margin is per customer tier and I say "I'll get back to you" and then I never do because the data doesn't exist.

**Sam:** Have you looked at any pricing tools?

**Customer C:** I talked to a pricing consultant who wanted $80K for a three-month engagement. I looked at tools like Stigg and Schematic but they handle the billing mechanics, not the analytics. Nobody helps me answer "what should I charge and will it work." I need the analysis layer, not just the plumbing.

**Sam:** What would make you move?

**Customer C:** If I could upload my usage data, define custom metrics like "insights generated," and run a simulation that shows me "if you switch to $2 per insight, here's the revenue impact by customer segment" — I'd sign up today. Then if the same tool could actually implement that pricing through Stripe, I'd pay whatever you charge. The simulation part is the real value. The billing part is table stakes.
