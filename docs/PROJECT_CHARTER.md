# Project Charter — VOC Trust & Lifecycle Friction Intelligence System

## 1) Project Name
VOC Trust & Lifecycle Friction Intelligence System (Public Demo)

## 2) One-Sentence Summary
A continuously updating ML-driven system that ingests public consumer complaints and produces executive-ready insights on trust-related customer friction (holds, account closures, unauthorized transactions, support failures), including prioritization and early warning signals.

## 3) Background / Context
Financial institutions and fintechs manage customer trust as a core business constraint. When trust breaks (e.g., account freezes, missing funds, unauthorized transactions), it drives churn, regulatory risk, and reputational damage. Internally, companies have customer support logs and surveys; externally, they lack a standardized and benchmarkable view of customer pain signals across the market.

This project uses the CFPB Consumer Complaint Database as a credible, public external signal and builds an ML-powered system to:
- Translate complaint records into lifecycle-aligned friction categories
- Prioritize high-trust-damage issues
- Forecast emerging issues and potential spikes
- Present insights in a VP-ready Streamlit dashboard and briefing format

## 4) Users and Stakeholders
Primary stakeholder audience (who the demo is built for):
- Product leaders (Manager/Director/VP)
- Operations and Customer Experience leaders
- Risk and Compliance leaders
- Executive stakeholders assessing trust and customer harm trends

Secondary audience:
- Data Science / Analytics teams (evaluate methods, interpretability, monitoring)

## 5) Problem Statement
Executives need a reliable, external, continuously updating view of trust-related friction:
- What is breaking trust right now?
- Where in the customer lifecycle is it breaking?
- Which issues are most severe and likely to escalate?
- What issues are trending upward and likely to spike next?

## 6) Goals (What “Success” Means)
Business goals:
- Provide a clear, decision-ready prioritization of trust frictions by company and timeframe
- Enable peer benchmarking (“How do we compare to similar institutions?”)
- Provide early warning on emerging/spiking issue categories

Technical goals:
- Build a robust data pipeline (ingest → clean → curate) that refreshes automatically
- Train ML components that are accurate enough to be credible, explainable, and stable
- Build a Streamlit app that loads quickly and communicates insights clearly

## 7) Non-Goals (Explicitly Out of Scope for v1)
- Diagnosing root causes using internal transaction logs (not available publicly)
- Making firm claims about causality (“X caused Y”) based only on complaint data
- Building a production-grade SaaS platform (this is a demo-quality “data product”)
- Detecting individual fraud events (aggregate analytics only)

## 8) Data Source(s)
Primary source (v1):
- CFPB Consumer Complaint Database (public)
Data types:
- Structured: company, product, issue/sub-issue, dates, response/timeliness markers
- Text: narrative text when available (opt-in; may be missing for many rows)

## 9) Target Use Cases (Examples)
- “Top trust frictions for Company X in the last 90 days”
- “Which trust frictions are rising fastest for Company X?”
- “Which friction types are predicted to spike next month?”
- “Peer benchmarking: Company X vs peer median for trust categories”
- “Priority queue: highest-severity complaint themes”

## 10) Proposed Solution Overview (System Components)
The system is built in layers:

A) Data Pipeline (Bronze/Silver/Gold)
- Bronze: raw ingested records
- Silver: cleaned, normalized, consistent schema
- Gold: aggregated tables optimized for dashboard + ML inputs

B) ML Layer A — Complaint Understanding
- Predict lifecycle stage + friction type (trust-first taxonomy)

C) ML Layer B — Severity / Escalation Scoring
- Assign severity score to prioritize trust-damaging complaints

D) ML Layer C — Early Warning
- Forecast weekly complaint volumes by friction category and detect spikes

E) Presentation Layer
- Streamlit dashboard for executives
- Optional briefing pack template for narrative delivery

## 11) Deliverables (Artifacts)
Data artifacts:
- Bronze/Silver/Gold Parquet tables

Model artifacts:
- Classification model (lifecycle stage + friction type)
- Severity scoring model (or severity index)
- Forecast outputs and spike alerts

Product artifacts:
- Streamlit app (public demo)
- Documentation: taxonomy, data dictionary, model cards, evaluation summary

## 12) Assumptions
- Complaint data is a useful external signal for trust friction and customer harm
- Complaint volume is not equal to customer base size; benchmarking must be interpreted carefully
- Missing narratives are expected; system must work with structured fields alone

## 13) Risks and Mitigations
Risk: Data is biased toward high-severity negative experiences
Mitigation: Treat outputs as “risk radar,” not overall satisfaction

Risk: Company naming inconsistencies create misleading comparisons
Mitigation: Normalize company names; maintain an alias mapping file

Risk: Narrative text availability varies over time and companies
Mitigation: Support “structured-only” models and optional “text-enhanced” models

Risk: Over-claiming to stakeholders
Mitigation: Clear disclaimers; emphasize "signal detection" and "prioritization", not causality

## 14) Operating Cadence (Continuous Updates)
- Daily/3x-week ETL refresh (pull new complaints, update curated tables)
- Daily scoring of new complaints (classification + severity)
- Weekly forecast refresh (update early warning)
- Monthly retraining (optional) or retrain-on-drift

## 15) Timeline (High-Level)
Phase 1: Pipeline + Streamlit MVP
Phase 2: Classification model
Phase 3: Severity scoring
Phase 4: Forecasting / early warning
Phase 5: Automation + polishing + stakeholder-ready packaging

(Exact schedule is flexible; quality is prioritized over speed.)

## 16) Definition of Done (v1)
- Streamlit app publicly deployed and stable
- Pipeline refresh automated and reproducible
- ML outputs are plausible, explainable, and documented
- Executive dashboard answers: “What broke trust, how severe, what’s rising, what’s next?”
