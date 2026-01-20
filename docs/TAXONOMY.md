# Taxonomy — Trust-First Lifecycle Stages and Friction Types (v0)

This taxonomy defines the categories our ML system will predict and the dashboard will use.
It is designed for executive readability and operational ownership.

Key principle:
- Lifecycle Stage answers: "Where in the customer journey did trust break?"
- Friction Type answers: "What exactly went wrong?"

We start with a trust-first emphasis. Growth-first categories can be added later without redesigning the system.

---

## 1) Lifecycle Stages (Trust-First)

### Stage 1 — Identity & Access (Account Access)
Definition:
- Problems logging in, verifying identity, account access disruptions, identity-related failures.
Examples:
- Locked out of account, login failures, identity verification problems that block access.

Typical owners:
- Security, IAM, Product (Auth flows), CX Ops

---

### Stage 2 — Money Availability & Holds (Funds Availability)
Definition:
- Customer cannot access their money when expected: holds, pending deposits, delayed availability, “funds missing” claims.
Examples:
- Deposit pending too long, funds not available after transfer, holds without clear explanation.

Typical owners:
- Payments Ops, Risk, Product (funds availability UX), CX Ops

---

### Stage 3 — Transactions & Money Movement (Payments/Transfers)
Definition:
- Problems sending/receiving money: transfers failing, payment declines, ACH/card issues (as reflected in complaint issues).
Examples:
- Transfer failed, payment reversed unexpectedly, repeated declines without explanation.

Typical owners:
- Payments Engineering, Payments Ops, Risk, Product

---

### Stage 4 — Unauthorized Activity & Fraud Claims (Trust Breach)
Definition:
- Customer reports unauthorized transactions, fraud, identity theft, disputed charges.
Examples:
- Unauthorized transfer, card used without permission, suspicious activity and insufficient remediation.

Typical owners:
- Fraud/Risk, Disputes, CX Ops, Compliance

---

### Stage 5 — Account Restrictions, Freezes, Closures (Account Trust Events)
Definition:
- Account closed, frozen, restricted; customer believes action was unfair/unclear.
Examples:
- Account closed without notice, locked due to suspected fraud but customer cannot regain access, closure impacts funds access.

Typical owners:
- Risk Policy, Compliance, CX Ops, Product (communications + appeals)

---

### Stage 6 — Disputes, Resolution & Customer Support (Resolution Journey)
Definition:
- Poor resolution outcomes: slow support, unclear responses, repeated handoffs, dissatisfaction with dispute handling.
Examples:
- Company did not respond, support unreachable, dispute denied without explanation.

Typical owners:
- CX Ops, Disputes Ops, Compliance Liaison, Product (support tooling)

---

### Stage 7 — Fees, Interest, Billing Confusion (Financial Harm Perception)
Definition:
- Unexpected fees, interest charges, billing confusion, refund problems, perceived unfair pricing.
Examples:
- Unexpected fees, interest applied incorrectly, refund delays.

Typical owners:
- Product, Billing Ops, Risk/Policy (where policy-driven), CX Ops

---

## 2) Friction Types (Trust-First)

We define friction types as action-oriented clusters. These are intended to be fewer than raw CFPB issues and more stable over time.

### FT1 — Funds Held / Not Available
Definition:
- Customer cannot access funds; delayed availability; holds.
Signals:
- “funds not available”, “hold”, “pending deposit”, “money missing”

### FT2 — Account Frozen / Restricted
Definition:
- Account access restricted due to risk or policy; customer blocked.
Signals:
- “frozen”, “restricted”, “locked”, “can’t access account”

### FT3 — Account Closed (Without Clear Resolution)
Definition:
- Account closed; customer dissatisfied with process, notice, fund access, appeals.
Signals:
- “closed”, “terminated”, “shut down”, “without notice”

### FT4 — Unauthorized Transaction / Fraud Claim
Definition:
- Customer alleges fraud/identity theft/unauthorized use.
Signals:
- “unauthorized”, “fraud”, “identity theft”, “not me”

### FT5 — Dispute/Chargeback Handling Failure
Definition:
- Customer disputes a transaction and perceives mishandling or denial without clarity.
Signals:
- “dispute denied”, “chargeback”, “investigation”, “no explanation”

### FT6 — Transfer Failed / Reversed / Pending Too Long
Definition:
- Transfers fail or remain pending; reversals confuse customers.
Signals:
- “failed transfer”, “pending”, “reversal”, “returned”

### FT7 — Declines / Payment Not Processed
Definition:
- Payment declines or doesn’t go through, often without clarity.
Signals:
- “declined”, “payment won’t go through”, “error”, “cannot pay”

### FT8 — Customer Support Unresponsive / Slow
Definition:
- Customer cannot reach support or resolution timeline is excessive.
Signals:
- “no response”, “unreachable”, “waiting”, “no help”

### FT9 — Fees / Interest / Billing Surprise
Definition:
- Unexpected fees/interest; confusion over charges; perceived unfair billing.
Signals:
- “fee”, “interest”, “charged”, “unexpected”

### FT10 — Communication & Transparency Failure
Definition:
- Customer claims company did not explain actions, policies, or outcomes.
Signals:
- “no explanation”, “unclear”, “no notice”, “no reason”

### FT11 — Verification / KYC Failure (Trust-Relevant)
Definition:
- Identity checks fail or create loops; customer cannot proceed or regain access.
Signals:
- “verify identity”, “KYC”, “documents rejected”, “selfie verification”

### FT12 — Refund / Charge Reversal Delays
Definition:
- Refunds delayed; merchant disputes; money not returned when expected.
Signals:
- “refund”, “not received”, “return”, “took weeks”

---

## 3) Mapping Notes (How we’ll use CFPB fields)
The CFPB dataset contains product/issue/sub-issue categories. We will:
- Use these structured fields for initial mapping where possible
- Use narrative text (when available) to refine or override with ML
- Maintain a mapping table: CFPB issue → lifecycle stage + friction type

This avoids dependence on any single field and makes the system resilient.

---

## 4) Growth-First Extension (Planned, Not Required for v1)
If we later add growth-first emphasis, we add additional lifecycle stages/friction types such as:
- Onboarding drop-off (application abandonment)
- Bank linking / funding setup failure
- Feature adoption friction (but only if data supports it)

We will not redesign the taxonomy; we will extend it.

---

## 5) Governance: How changes to taxonomy are handled
Taxonomy changes are versioned:
- v0, v1, v2…
Each change must include:
- rationale (“why”)
- impact assessment (what model outputs change)
- backfill plan (re-score historical data if needed)
