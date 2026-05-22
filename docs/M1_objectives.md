# Project Objectives — Santander Customer Transaction Prediction

**Team:** Hanish (PM), Vasyl (modeling), Roland (research)
**Timeline:** Day 1 kickoff → Day 4 presentation

## What we're building, in one sentence

A model that helps Santander figure out which customers are likely to make a transaction in the near future — so the bank can reach out at the right moment instead of guessing.

## Why this matters

Right now, banks waste a lot of effort marketing to customers who weren't going to act anyway. If we can predict who's likely to make a transaction, Santander can be more helpful and less annoying: better-timed offers, fewer mass emails, more relevant suggestions. This ties directly to Santander's stated goal of helping customers understand their financial health.

## What the model actually does

For each customer, it outputs a number between 0 and 1 — basically, *how likely* is this person to make the transaction. It's not a yes/no answer; it's a probability. Higher means more likely.

## How we measure success

**Main metric: ROC-AUC.** It measures how well the model can sort customers from "least likely" to "most likely." A perfect model scores 1.0; random guessing scores 0.5.

We are *not* using accuracy. Here's why: only about 10% of customers will actually make a transaction. So a "model" that just says "nobody will act" is 90% accurate — and completely useless. ROC-AUC doesn't fall for that trick.

We also track PR-AUC as a sanity check — it's another metric that handles imbalanced data well.

## What we're comparing against

**The floor:** Predict "no transaction" for everyone. Expected ROC-AUC = 0.5. If we don't beat this, we have nothing.

**The bar:** A basic logistic regression that accounts for the class imbalance. We expect it to score around 0.7. Anything we build should clearly beat this.

## What "done" looks like

| Goal | Good | Great |
|---|---|---|
| Final model ROC-AUC | ≥ 0.85 | ≥ 0.90 |
| Beats the logistic baseline by | 5+ points | 10+ points |
| Code runs end-to-end with one command | Yes | — |
| Presentation length | 12 minutes or less | — |
| Slides understandable without ML jargon | All slides | — |

## What we're NOT doing

- Solving the known synthetic test rows (flagged as future work)
- Hyperparameter tuning rabbit holes (one focused round, max)

## Things to watch out for

- Vasyl is out Monday and we're not working weekends — the baseline must be ready by end of Day 1 - Day 2 midday, or Monday becomes blocked
- Features are anonymized (var_0, var_1, etc.) — we can't tell stories about specific features; we'll lean on overall feature importance instead
- Kaggle's 50/50 train/test split is unusual; their test file has no labels, so we'll split our own training data 80/20 for validation

---

## Final Outcomes (added post-project)

This section was added after the project completed, comparing what we set out to do against what we actually delivered.

### Did we hit our success criteria?

| Goal | Target (Good) | Target (Great) | Actual | Result |
|---|---|---|---|---|
| Final model ROC-AUC | ≥ 0.85 | ≥ 0.90 | **0.890** | ✅ Good, just shy of Great |
| Beats logistic baseline by | 5+ points | 10+ points | **2.4 points** | ❌ Below target |
| End-to-end reproducibility | Yes | — | 🔄 Notebooks reproducible; full `.py` refactor flagged as Future Work | Partial |
| Presentation length | ≤ 12 min | — | 12 min | ✅ |
| Slides understandable without ML jargon | All slides | — | All slides | ✅ |

### Where we missed and why

**The 2.4-point gap between baseline and main model is smaller than we'd hoped.** Our M1 estimate predicted the baseline at ~0.7 and the main model at ~0.9 (a ~20-point gap). What actually happened: logistic regression scored 0.866 — much stronger than expected on this dataset — leaving less headroom for LightGBM to clearly outperform. This isn't a failure of the LightGBM model; it's a sign that the dataset's signal is more accessible to linear models than we assumed.

**The 0.90 target was missed by 0.01.** Documented in our critical review with three concrete next steps that would close the gap (frequency encoding, cross-validation, hyperparameter tuning).

### What we did better than expected

- **The critical review notebook** was an unplanned addition that became the strongest single artifact in the project. It's referenced in our presentation, this document, and the decisions log.
- **Process discipline** — we never deviated from the Explore → Prepare → Model → Review sequence, and never let modeling results leak back into preparation. This wasn't a given on a 4-day timeline.
- **Honest documentation** — every major choice is logged in `decisions_log.md` with the rationale at the time, not reconstructed after the fact.

### What we'd commit to next time

- Anchor M1 baseline estimates on prior public benchmarks, not gut feel. Our logistic estimate was off by ~15 ROC-AUC points, which reframed the whole project.
- Plan a `.py` refactor block into the timeline from Day 1 rather than leaving it to Day 4. It got squeezed by presentation prep.
- Start the critical review notebook earlier (during modeling, not after) so it informs late-stage decisions rather than just documenting them.

For full retrospective material, see [reflection.md](reflection.md).