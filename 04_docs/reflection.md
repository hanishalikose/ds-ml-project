# Reflection — Running Log

A log of what we learned across the project. Becomes the raw material for next week's team retrospective.

## How to add an entry

```
### [Day] — Short label
What happened: ...
What we learned: ...
What to do about it: ...
```

---

### [Day 4] — Final deliverables and presentation prep
**What happened:** Built the final 12-slide deck (Santander challenge → trap → north star → findings → results → reflections → lesson → close). Wrote speaker notes for non-technical audience. Rehearsed once as a team.

**What we learned:** Building slides backward from the *lesson* ("process discipline beat the score") forced clarity on every other slide. When we knew where we were ending, the middle wrote itself. We also learned that the critical_overview notebook was the single most valuable artifact for the presentation — without it, the "what we'd improve" slide would have been generic.

**What to do about it:** In future projects, decide the *closing message* before drafting any other slide. And always produce a critical review notebook alongside the model notebook — they pair naturally.

---

### [Day 3] — Modeling + self-review
**What happened:** Vasyl trained LightGBM with `class_weight='balanced'`, landed at 0.8899 ROC-AUC (target was 0.90, missed by 0.01). Built the critical_overview notebook documenting what we did well, what we'd improve, and the path to 0.92+. Drafted slides.

**What we learned:** The honest self-review was uncomfortable but clarifying. Listing weaknesses *before* anyone asked us forced us to actually understand them — not just acknowledge them. We also learned that the famous "frequency encoding" trick on this dataset was something Vasyl spotted independently while looking at the data (features have many repeated values), even before reading Kaggle notebooks. That was a real moment of "we're thinking about this the right way."

**What to do about it:** Critical review goes in every ML project from now on — it's a small time investment relative to the credibility it creates. And we should encourage more "noticing weird patterns" during EDA — Vasyl's instinct about repeated values was worth a dozen tuning passes.

---

### [Day 2] — EDA + feature engineering + baseline
**What happened:** Vasyl ran full EDA (notebook 01) and feature engineering (notebook 02). Confirmed 9:1 class imbalance, no strong individual features (max correlation 0.08), no missing data. Built six aggregate features that turned out not to help. Trained logistic regression baseline (0.866 ROC-AUC). Roland researched top Kaggle notebooks.

**What we learned:** Two big things. First, our M1 estimate for the logistic baseline (~0.7) was way off — the actual baseline was 0.866. Either logistic regression is stronger on this dataset than expected, or our estimate was conservative. Either way, we should anchor M1 estimates more carefully next time. Second, not every feature engineering idea works — the aggregate features had ~0.02 correlation with target. Keeping them in the pipeline was an educational choice, not a performance one.

**What to do about it:** In future M1 docs, estimate baselines from prior public benchmarks rather than gut feel. And be explicit when an engineered feature is included for learning vs. for performance.

---

### [Day 1] — Project kickoff
**What happened:** First team meeting. Picked Santander Customer Transaction Prediction over Mercedes-Benz and others. Set roles: Hanish (PM/docs), Vasyl (modeling), Roland (research). Built the GitHub Project board with 6 milestones and 5 labels. Drafted M1 objectives doc. Decided to compress baseline timeline to Day 1 because Vasyl was out Monday and no weekend work was agreed.

**What we learned:** Two things, actually. First, the role split mapped cleanly to individual strengths — we didn't have to negotiate who did what after the first hour. Second, surfacing the "Vasyl out Monday + no weekend work" risk on Day 1 saved us. Without that being visible, we'd have hit a wall mid-project.

**What to do about it:** Always do the scheduling risk-check during kickoff, not in the middle of the project. Even on a 4-day timeline, a 15-minute conversation about who's available when changes the whole plan.

---

## Team-level themes across all four days

**Process discipline genuinely paid off.** Day 1 was data understanding only. Day 2 was the first model. We never reversed the order. When we hit the 0.89 result on Day 3, we didn't panic and chase tricks — we wrote a critical review instead. That sequence of choices is what made our presentation defensible.

**The PM role was load-bearing on this project.** Three-person team, asymmetric availability, multiple deliverables, a tight clock. Without explicit ownership of the project board, milestones, decisions log, and presentation, things would have drifted. PM work is invisible when it's done well — visible only when it's not.

**Honest self-review is undervalued in cohorts.** Our critical_overview notebook took maybe two hours to write. Almost no team produces one. The asymmetric return on that two hours — both for our own understanding and for how the presentation reads — was the biggest leverage point of the project.

**Anonymized features have trade-offs we didn't fully appreciate in advance.** Yes, you can still build a model. But you can't tell stories about specific features, you can't sanity-check engineered features intuitively, and you lose the most natural way of explaining results to non-technical stakeholders. Next time, factor this in when choosing a dataset.