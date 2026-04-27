# Demo Call — Acme AI and Customer A

**Date:** 2026-03-15
**Participants:** Sam Rivera (Acme AI CEO), Customer A (Head of Product, NovaTech)
**Duration:** 25 minutes

---

**Sam:** Thanks for jumping on. I'd love to hear how you're handling pricing right now.

**Customer A:** We're an AI writing assistant. We charge a flat $99 a month per seat, but our costs per customer vary wildly. Some customers use 10x more tokens than others. We have no idea what our actual margin is per customer. We just look at the aggregate Stripe revenue and subtract our OpenAI bill and hope the number is positive.

**Sam:** How do you track token costs?

**Customer A:** We don't, really. Our CTO built a script that pulls from the OpenAI usage API once a day and dumps it into a Google Sheet. It shows total spend but not per-customer. If I want to know what Customer X costs us, I have to go ask an engineer to query the database. That takes a day and the answer is always approximate.

**Sam:** What happens when a heavy user shows up?

**Customer A:** We had a customer last quarter who was generating 50,000 words a day. Our average is about 2,000. We didn't notice for three weeks because nobody monitors per-customer usage. By the time our CTO flagged it, they'd burned through $4,000 in API costs on a $99 subscription. That's a 40x negative margin. We couldn't even retroactively charge them because our pricing model doesn't have usage limits.

**Sam:** Have you looked at usage-based pricing?

**Customer A:** We've talked about it for six months. The problem is we don't know how to implement it. Our billing is Stripe subscriptions with fixed plans. Moving to usage-based means we need metering, we need to track tokens per customer in real time, we need to figure out pricing tiers, and then we need to actually change the Stripe integration. Our engineers quoted it at three months of work. Meanwhile we're losing money on heavy users every day.

**Sam:** What would change if you could see per-customer margins today?

**Customer A:** I'd immediately know which pricing tier each customer should be on. Right now I'm guessing. I think maybe 10% of our customers are unprofitable, but I literally cannot prove it. If I could see a dashboard that shows revenue minus cost per customer, I'd restructure our pricing within a week. The data would make the decision obvious. Without it, I'm just arguing with my co-founder about gut feelings.

**Sam:** Would you pay for a tool that did this?

**Customer A:** We're currently paying an engineer half their time to maintain billing scripts. That's probably $75,000 a year in engineering time. If a tool could give us per-customer margin visibility, usage tracking, and help us move to usage-based pricing, I'd pay $1,000 a month without blinking. That's a fraction of what we're spending now on the duct tape solution that doesn't even work.
