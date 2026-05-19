# Decisions Log

A running list of choices we've made and why. Add new entries at the top so the most recent is always first.

## How to add an entry

```
### [Date] — Short title
We decided to: ...
Because: ...
Who: who proposed
```

---

## Decisions so far

### [Day 1] — Use ROC-AUC as the main metric, PR-AUC as backup
We decided to optimize for ROC-AUC and track PR-AUC alongside it.
Because: Kaggle scores on ROC-AUC, and accuracy is a trap when only 10% of customers are positive. PR-AUC gives us a second honest measure.
Who: Team.

### [Day 1] — Logistic regression for baseline, LightGBM for the improvement
We decided to start with logistic regression (simple, interpretable) and try LightGBM as our better model.
Because: Logistic regression gives us a clear bar to beat. LightGBM handles imbalanced data and different feature scales without preprocessing, and it's known to perform well on this dataset.
Who: Vasil.

### [Day 1] — Split train.csv 80/20 ourselves, ignore test.csv for validation
We decided to take the file Kaggle calls train.csv, split it 80/20 (keeping the same class balance in both pieces), and use that for all our evaluation.
Because: Kaggle's test.csv has no labels — we couldn't score ourselves on it. Their setup is for competition submission, not internal validation.
Who: Team.

### [Day 1] — Stick to the 5 bootcamp Kanban labels
We decided to use only EDA, Modeling, Evaluation, Presentation, and Planning. No extras.
Because: Matches the bootcamp's recommended setup. More labels = more noise on a 4-day project.
Who: Hanish.

### [Day 1] — Ship baseline by end of Day 1, not Day 2
We decided to compress the baseline timeline so it's ready before the weekend.
Because: Vasil (our modeler) is out Monday and we're not working weekends. If the baseline isn't ready Friday, Monday becomes a dead day. Pulling it forward keeps the team productive without him.
Who: Hanish.