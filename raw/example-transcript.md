# Demo Call — StreamLine and Alex Chen

**Date:** 2026-03-15
**Participants:** Jordan Taylor (StreamLine CEO), Alex Chen (VP Engineering, Patchwork)
**Duration:** 28 minutes

---

**Jordan:** Thanks for jumping on this, Alex. I'd love to hear about what your team's dealing with on the project management side.

**Alex:** Yeah, so we're at about 60 engineers now, split across seven teams. We use Linear for tickets, but honestly, every team tracks things a little differently. Some teams are diligent about story points, others just throw tickets in and never estimate. So when leadership asks me "what's our velocity?" I basically have to pull data from seven different projects and try to reconcile it in a spreadsheet.

**Jordan:** How long does that take you?

**Alex:** Probably four to five hours every two weeks. And the numbers are always wrong because teams update their tickets at different times. I'm basically reporting velocity from two sprints ago because that's the last time the data was clean enough to use.

**Jordan:** What happens when the numbers are wrong?

**Alex:** We make bad staffing decisions. Last quarter we thought Team Atlas was underperforming, but it turned out they were doing tons of untracked work — code reviews, incident response, mentoring. We almost pulled their tech lead off to another team before someone caught it. That would have been a disaster.

**Jordan:** Have you tried any tools to fix this?

**Alex:** We tried Jellyfish for about three months. The data was good but it cost us $48,000 a year and nobody except me actually logged into it. Forty-eight thousand dollars for a dashboard only one person uses. We cancelled it. Before that we tried building something internal with Metabase, but the engineer maintaining it left and nobody wanted to take it over.

**Jordan:** So what do you do now?

**Alex:** Google Sheets. I have a monster spreadsheet with macros that pulls from the Linear API. It breaks every time Linear changes their API, which is about once a month. Last month it double-counted a bunch of tickets because Linear changed how they handle subtasks. I spent a whole afternoon debugging a spreadsheet formula instead of doing my actual job.

**Jordan:** If you could wave a magic wand, what would you want?

**Alex:** I want one number per team per sprint that I can trust. Not a dashboard with forty charts. One number that tells me "Team Atlas delivered X story points this sprint, here's the trend." And I want to know when a team is quietly drowning — like when they're spending 60% of their time on unplanned work and nobody's flagging it.

**Jordan:** Would you pay for that?

**Alex:** Honestly, yes. I'd pay out of my own budget, not even go through procurement. If you could give me reliable cross-team velocity for under $500 a month, I'd sign today. The $48K we spent on Jellyfish proves there's budget for this, we just need something that actually gets used.

**Jordan:** What about your CTO? Would they need to approve it?

**Alex:** My CTO would approve anything that stops me from sending her wrong numbers. Last board meeting I had to correct a velocity chart mid-presentation. She was not happy. If I came to her with a tool that gives clean numbers automatically, she'd approve it in five minutes.

**Jordan:** How do you handle it when a team pushes back on being measured?

**Alex:** That's the hardest part. Some engineers see velocity tracking as surveillance. Team Nebula's lead literally told me "story points are made up and you're using them to judge us." He's not wrong that story points are imperfect, but I still need something. I'd love a way to frame this as helping teams rather than monitoring them — like showing each team their own trends so they can self-improve rather than having me report on them to leadership.

**Jordan:** That's a really interesting framing. More like a fitness tracker for teams than a surveillance camera.

**Alex:** Exactly. If each team lead could see their own data and make their own decisions, I wouldn't need to be the velocity police. Right now I'm the bad guy because I'm the one who shows up with the spreadsheet.

**Jordan:** One last question — if we built this, how would you want to get the data in? API integration with Linear? CSV upload?

**Alex:** API integration or I'm not interested. I'm done with manual data entry. We already have Linear, GitHub, and PagerDuty. If your tool can pull from those three, you have everything you need. If I have to manually enter anything, it'll die like every other internal tool we've tried.
