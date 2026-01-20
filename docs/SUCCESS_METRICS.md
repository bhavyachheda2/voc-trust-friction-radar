# Success Metrics — VOC Trust & Lifecycle Friction Intelligence System

This document defines how we judge success from:
1) business stakeholder usefulness,
2) model performance, and
3) operational reliability.

The project is a data product, not a single notebook. Success must include "works reliably" and "communicates clearly."

---

## 1) Business / Stakeholder Success Metrics (Primary)
These are the most important because the intended audience is executives and leaders.

### 1.1 Decision Readiness
A stakeholder should be able to answer these within 2 minutes in the dashboard:
- What are the top trust frictions for Company X in the last 90 days?
- Which trust frictions are trending upward right now?
- What should we fix first (highest severity / highest business risk)?
- What is likely to spike in the next 2–4 weeks?

Success indicator:
- The dashboard yields a clear top-3 prioritization with evidence (trend + counts + severity).

### 1.2 Actionability
Outputs should map to realistic owners:
- Risk/Compliance (unauthorized transactions, account takeover symptoms, disputes)
- Ops/CX (response delay, support failures)
- Product (holds UX, account closure comms, onboarding and verification issues)

Success indicator:
- For each top friction type, the dashboard can suggest “owner” and “what to investigate next.”

### 1.3 Executive Credibility
Success indicator:
- The narrative is defensible (no over-claims of causality)
- Clear limitations are stated (complaints are a negative-signal dataset)
- Benchmarking is presented carefully (peer context, trends rather than absolute judgments)

---

## 2) Model Success Metrics (Secondary, but important)
We have three ML components. Each has its own evaluation approach.

### 2.1 ML Layer A — Classification (Lifecycle Stage + Friction Type)
Technical metrics:
- Macro F1 score (handles class imbalance)
- Per-class precision/recall for key “trust” categories
- Confusion matrix review for common misclassifications

Practical acceptance criteria (v1):
- Key trust categories (e.g., account closure, funds held, unauthorized transactions, support failures) achieve strong recall (we prefer catching them over missing them).
- Misclassifications are explainable and not obviously wrong at scale.

Why:
In trust/risk contexts, missing severe categories is worse than occasionally over-flagging.

### 2.2 ML Layer B — Severity / Escalation Scoring
Two possible approaches: supervised model or calibrated severity index. Evaluation depends on approach.

If supervised:
- AUC / PR-AUC (if labels are imbalanced)
- Calibration curve (predicted probability aligns with observed outcomes)
- Top-k precision (do the top 50 “most severe” look severe?)

If index:
- Face validity checks (top-ranked complaints match known severe patterns)
- Stability over time (severity distribution doesn’t fluctuate wildly without reason)
- Correlation with available outcome proxies (e.g., dispute indicator where available)

Practical acceptance criteria (v1):
- Top-k review: a human review of top 50 must be “credible” (high trust damage).
- Severity score provides useful ranking, not just a number.

### 2.3 ML Layer C — Early Warning Forecasting
Metrics:
- MAE/MAPE on backtests (rolling-origin evaluation)
- Spike detection precision/recall on historical surges (define “spike” threshold)

Practical acceptance criteria (v1):
- Forecast trends are directionally correct and not erratic.
- Spike alerts are not overly noisy (false alarms undermine trust).

---

## 3) Data & Pipeline Reliability Metrics (Must-Have)
These are corporate necessities; if these fail, the product is not usable.

### 3.1 Data Freshness
- Last refresh timestamp displayed in dashboard
- Expected refresh cadence achieved (daily or 3x/week)

### 3.2 Data Quality Checks (automated)
Minimum checks:
- Row count non-zero and within expected range
- Date range increases over time
- Key columns present (schema validation)
- Missingness monitored (e.g., % narrative present)
- Company normalization coverage (no explosion of company name variants)

### 3.3 Performance
- Streamlit dashboard loads within ~2 seconds for core views (using gold tables)
- ETL runtime reasonable (target < 10–15 minutes for scheduled job)

---

## 4) Documentation & Governance (Credibility Multipliers)
These are not “metrics,” but are required for stakeholder trust.

Required:
- Data dictionary (fields used, definitions, caveats)
- Taxonomy doc (lifecycle stages and friction types, with examples)
- Model cards (what the model does, limitations, known failure modes)
- Monitoring plan (what triggers retraining, what drift checks exist)

Success indicator:
- A reviewer can understand the system without reading code first.

---

## 5) “Do we ship?” Checklist (v1)
We ship v1 when:
- Pipeline refresh works end-to-end
- Dashboard answers the 4 executive questions
- Classification labels are plausible and documented
- Severity ranking appears credible in top-k review
- Forecasting outputs pass backtest sanity checks
- Clear disclaimers and limitations are included in the app
