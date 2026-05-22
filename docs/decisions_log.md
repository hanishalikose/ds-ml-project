# Decisions Log

A running list of choices we made and why. Most recent entries at the top.

## How to add an entry

```
### [Day] — Short title
We decided to: ...
Because: ...
Who: who proposed
```

---

## Day 4 — Final deliverables

### [Day 4] — Present at 0.89 rather than chase 0.90 with last-minute changes
We decided to land at our actual ROC-AUC of 0.8899 and present it honestly rather than attempting frequency encoding or last-minute hyperparameter tuning before the presentation.
Because: We had a fully reviewed, reproducible pipeline at 0.89. Pushing for 0.90 with a technique nobody on the team had time to fully understand would have risked the presentation deliverable. We chose to ship something we can fully defend over a marginally better score we couldn't.
Who: Hanish (PM call after reviewing critical_overview).

### [Day 4] — Build the presentation around "process discipline beat the score"
We decided to lead the presentation with our methodology and self-review, not the model score.
Because: The bootcamp explicitly values process over complexity. We had a stronger story to tell about *how* we worked than about our final number. The critical_overview notebook gave us material no other team is likely to have.
Who: Team consensus, anchored by Hanish.

---

## Day 3 — Modeling, threshold, and self-review

### [Day 3] — Use F1-optimal threshold (~0.60) instead of default 0.5
We decided to tune the prediction threshold for our LightGBM model and report 0.60 as the recommended operating point.
Because: With ~10% positive class, the default 0.5 cutoff is biased toward predicting "no transaction." Tuning the threshold improves the F1 score and makes individual predictions actionable. ROC-AUC is unaffected, but the deployed model is more useful at 0.60.
Who: Vasyl (modeling lead).

### [Day 3] — Do not attempt frequency encoding within the project window
We decided not to add frequency-encoded features even though they're known to push scores past 0.92 on this dataset.
Because: Implementing it cleanly within the remaining time risked breaking our pipeline, and we'd already established that we wouldn't push for ad-hoc improvements after the M5 freeze. Documented as the top item in Future Work instead.
Who: Team consensus.

### [Day 3] — Do not implement cross-validation
We decided to evaluate on our single stratified 80/20 split rather than 5-fold cross-validation.
Because: CV would have required restructuring 03_modeling.ipynb and re-running both models — time we needed for the critical review and slides. Documented as second priority in Future Work.
Who: Vasyl.

### [Day 3] — Write a separate critical_overview notebook for self-review
We decided to add a fourth notebook explicitly dedicated to honestly critiquing our own work, separate from the modeling notebook.
Because: Self-review is one of the bootcamp's nice-to-have PM tasks, and we wanted the artifact to be visible and defensible. Forces clarity on what we'd genuinely improve.
Who: Hanish (PM proposal), executed by team.

---

## Day 2 — EDA, feature engineering, baseline

### [Day 2] — Use RobustScaler instead of StandardScaler
We decided to scale features with RobustScaler (centered on the median, scaled by IQR) rather than the more common StandardScaler.
Because: Our EDA showed some features have outliers we couldn't easily distinguish from real extreme values (anonymized data — we don't know what's plausible). StandardScaler is sensitive to outliers; RobustScaler isn't. The trade-off is that scaled output doesn't have mean 0 / std 1 — it has median 0 / IQR 1.
Who: Vasyl.

### [Day 2] — Add six aggregate row-wise features
We decided to engineer six new features per customer: row_mean, row_std, row_min, row_max, row_range, row_skew across all 200 original features.
Because: With no single feature being strongly predictive (max correlation ~0.08), we wanted to see if summary statistics about a customer's profile would help. Spoiler from the critical review: they didn't (correlation with target ~0.02). We kept them for the educational record.
Who: Vasyl.

### [Day 2] — Save both scaled and unscaled versions of train/val data
We decided to maintain two copies of the processed data — scaled for logistic regression, unscaled for LightGBM.
Because: LightGBM is tree-based and doesn't need scaling. Logistic regression requires it. Saving both prevents accidental misuse and makes downstream notebooks cleaner.
Who: Vasyl.

---

## Day 1 — Project setup and framing

### [Day 1] — Use ROC-AUC as the main metric, PR-AUC as backup
We decided to optimize for ROC-AUC and track PR-AUC alongside it.
Because: Kaggle scores on ROC-AUC, and accuracy is a trap when only 10% of customers are positive. PR-AUC gives us a second honest measure.
Who: Team.

### [Day 1] — Logistic regression for baseline, LightGBM for the improvement
We decided to start with logistic regression (simple, interpretable) and try LightGBM as our better model.
Because: Logistic regression gives us a clear bar to beat. LightGBM handles imbalanced data and different feature scales without preprocessing, and it's known to perform well on this dataset.
Who: Vasyl.

### [Day 1] — Split train.csv 80/20 ourselves, ignore test.csv for validation
We decided to take Kaggle's train.csv, split it 80/20 (keeping the same class balance), and use that for all our evaluation.
Because: Kaggle's test.csv has no labels — we couldn't score ourselves on it. Their setup is for competition submission, not internal validation.
Who: Team.

### [Day 1] — Stick to the 5 bootcamp Kanban labels
We decided to use only EDA, Modeling, Evaluation, Presentation, and Planning. No extras.
Because: Matches the bootcamp's recommended setup. More labels = more noise on a 4-day project.
Who: Hanish.

### [Day 1] — Ship baseline by end of Day 1, not Day 2
We decided to compress the baseline timeline so it was ready before the weekend.
Because: Vasyl (our modeler) was out Monday and we agreed no weekend work. If the baseline wasn't ready Friday, Monday would be a dead day. Pulling it forward kept the team productive without him.
Who: Hanish.