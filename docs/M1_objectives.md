# Project Objectives — Santander Customer Transaction Prediction

**Team:** Hanish (PM), Vasil (modeling), Roland (research)
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

- Solving the known synthetic test rows (we'll flag it as future work)
- Hyperparameter tuning rabbit holes (one focused round, max)

## Things to watch out for

- Vasil is out Monday and we're not working weekends — the baseline must be ready by end of Day 1 - Day 2: midday, or Monday becomes blocked
- Features are anonymized (var_0, var_1, etc.) — we can't tell stories about specific features; we'll lean on overall feature importance instead
- Kaggle's 50/50 train/test split is unusual; their test file has no labels, so we'll split our own training data 80/20 for validation