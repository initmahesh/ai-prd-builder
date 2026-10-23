# PRD.md: Contract Risk and Monetization Platform

A complete example PRD that passes the checklist. Use it as a pattern for structure and depth, never as content for another product. Numbers marked proposed are starting values; items marked SET need the user's confirmation.

Version: 0.1 | Owner: Mahesh Yadav | Status: Draft | Updated: 2026-10-22
Spec change log: every edit to this file is recorded at the bottom (section 6).

## 0. How to use this file

For people: read sections 1 and 2 for the why and the experience, 3 and 4 for what must be true to build and ship.
For coding agents: build only what is in scope (2.6). Every requirement has an ID (R-xx).
If a requirement is ambiguous, conflicts with the constitution (2.4), or needs a tool or permission not listed in 3.2, STOP and ask a human. Do not guess.
A requirement is done only when its evals in 3.4 and 3.5 pass.
Build order: 3.1 R-01 to R-04 (pre-signing slice, shadow mode) first; post-signing slice after the pre-signing gate in 4.1 passes.

## 1. DISCOVER

### 1.1 North Star and roadmap
North Star: every signed contract's commercial terms reach billing and sales systems correctly within 24 hours, with a lawyer's risk review done before signature.
Roadmap (each step unlocks the next):
1. Pre-signing redline in Outlook on one contract type, shadow mode (lawyers see output beside their own work).
2. Pre-signing redline live for design-partner customers.
3. Post-signing term extraction with human approval before any write to NetSuite or Salesforce.
4. Post-signing writes with selective auto-approval for low-risk terms.
5. More contract types and customers; usage-based pricing.

### 1.2 Problem and user evidence
Problem: legal teams spend hours on first-pass review and redlining. After signing, key commercial terms (price, term, renewal, escalators) are rarely entered into finance and sales systems correctly, so revenue is missed or delayed.
Evidence to attach before launch: SET interview count and quotes; hours per contract today; share of signed contracts with missing or wrong terms in NetSuite or Salesforce; revenue leakage estimate.

### 1.3 Why now and why us
Why now (confirm each with a source): SET model capability to read and redline long contracts; APIs for Outlook, DocuSign, NetSuite, Salesforce available; cost per contract now low enough to price profitably; customer pressure to protect revenue.
Why us: LegalGraph's contract knowledge graph and ontology, domain experience in legal operations, and integration into the systems finance already uses. SET add proof points.

### 1.4 Gap test: why not ChatGPT or Claude Code
1. Restrictions: customers in regulated or government settings cannot send contracts to a general consumer tool; we run inside their approved environment. SET confirm with 3 customers.
2. Shared learning: playbook rules and corrections from one reviewer improve results for the whole customer; a general chat does not accumulate this.
3. Long-horizon craft: contract review follows a specific plan (identify type, map clauses, apply playbook, redline, summarize risk) that a generic assistant does not hold.
4. Quality from data and ontology: results come from the knowledge graph of parties, clauses, obligations, and terms, not from the contract text alone.
5. Accountability and security: audit log, access control, and a vendor answerable for quality and safety.
Pass rule: if fewer than 3 of 5 hold for a target customer, do not sell to that customer.

### 1.5 Riskiest assumption
Assumption: lawyers will accept a redline they did not write if they can see how it was produced and verify it quickly.
Test first: shadow-mode study with 5 lawyers and 30 contracts. Kill or change the product if acceptance of suggested changes is under 60% (proposed).

### 1.6 Success metrics
- Median first-pass review time: down 50% vs. baseline (proposed).
- Redline acceptance rate by lawyers: 70% or more (proposed).
- High-risk clause recall: 95% or more (proposed).
- Key-term extraction field accuracy: 95% or more (proposed).
- Signed contracts with terms in NetSuite and Salesforce within 24 hours: 95% (proposed).
- Gross margin per contract after run cost: SET target.

### 1.7 MEP: minimum evaluable product
One contract type (SET, for example master services agreement), one customer playbook, 8 extraction fields (price, term, start date, renewal, auto-renew notice, escalator, payment terms, termination), 25 labeled contracts as ground truth. The MEP is ready to ship to design partners only when it passes the gate in 4.1.

### 1.8 Competitive context
Contract lifecycle tools and e-signature platforms exist. We differ by covering both pre-signing review and post-signing monetization, grounded in an ontology. Details live in the strategy doc, not here.

## 2. DESIGN

### 2.1 Users and roles
| Role | Needs | Authority |
| --- | --- | --- |
| In-house lawyer | Fast first-pass review, trust in each change | Approves or rejects every redline; final say on risk |
| Contract manager | Clean extraction of terms after signing | Approves terms before they are written downstream |
| Finance and billing ops | Correct terms in NetSuite | Reads results; flags errors |
| Sales operations | Correct terms in Salesforce | Reads results; flags errors |
| Customer admin | Controls access and playbook | Sets playbook, permissions, and spend limits |

### 2.2 Journeys
Pre-signing:
1. Lawyer opens a contract email in Outlook and clicks Review.
2. System identifies contract type, maps clauses, applies the customer playbook, and prepares a redline.
3. System PAUSES if confidence is low or a never-do rule applies (see 2.4) and asks the lawyer.
4. A draft redline document is saved in Outlook drafts, with a review panel (2.3). Nothing is sent.
5. Lawyer validates flagged items, edits, and sends on their own.

Post-signing:
1. DocuSign marks an envelope complete and triggers the system.
2. System fetches the signed document and extracts the 8 key terms.
3. System shows each term with its source passage and confidence to the contract manager.
4. Manager approves, edits, or rejects. Only approved terms are written to NetSuite and Salesforce.
5. System confirms the write, logs it, and reports any mismatch.

### 2.3 Trust design (layered)
Every result shows the answer first, then lets the user drill in:
- L1 Answer: the redline or the extracted terms, with an overall confidence label.
- L2 Plan: the steps followed (type identified, clauses mapped, playbook rules applied).
- L3 Knowledge used: the clauses, playbook rules, and ontology entries relied on, each linked to its source text.
- L4 Iterations: what was tried and changed, including rules that were overridden.
- L5 Checks: the evaluations run on this result and whether each passed.
- Always visible: what the system is sure of, what it is not sure of, and a short list of items needing the human to validate, with one-click accept, edit, or reject.
Rule: never show a bare answer without L1 confidence and the validate list.

### 2.4 Constitution
Never do:
- Send, sign, or share a contract or any email.
- Write to NetSuite or Salesforce without recorded human approval (until 4.4 allows otherwise).
- Invent a clause, number, party, or date that is not in the document.
- Give legal advice outside the customer playbook.
- Use one customer's data or playbook for another customer.
Priority order when rules conflict: 1 safety and confidentiality, 2 honesty about uncertainty, 3 playbook compliance, 4 helpfulness and speed.
Tone and output: plain business English, short sentences, cite the clause number for every claim, label uncertainty as High, Medium, or Low confidence, redlines in tracked-change format.
Escalation rules (stop and ask a human):
| Trigger | Who is asked | Behavior while waiting |
| --- | --- | --- |
| Confidence Low on a high-risk clause | Lawyer | Mark as needs review; make no change |
| Clause not covered by playbook | Lawyer | Flag; suggest nothing |
| Extracted term conflicts with another term | Contract manager | Hold the write |
| Contract type unknown | Lawyer | Stop and ask |
| Tool call fails twice | Customer admin | Stop; report error |
| Request outside intended use (4.5) | Customer admin | Refuse and log |

### 2.5 Examples
Good: lawyer-approved redline that changes a 12-month auto-renewal notice to 60 days per playbook, cites clause 9.2, marks confidence High.
Bad: redline that adds a liability cap not in the playbook and does not cite a clause. Must fail the honest check.
Borderline: a clause with unusual indemnity wording. Expected behavior: flag with Medium confidence, propose no edit, ask the lawyer.

### 2.6 Scope
In: Outlook review, redline, DocuSign trigger, 8-field extraction, human approval, NetSuite and Salesforce writes, audit log, dashboards.
Out: drafting contracts from scratch, sending email, other e-signature tools, other ERPs and CRMs, negotiating with counterparties.
Later: more contract types, auto-approval for low-risk terms, customer-facing reports.

## 3. DEVELOP

### 3.1 Requirements
| ID | Requirement | Done when |
| --- | --- | --- |
| R-01 | Read a contract attachment from an Outlook email the user selects | Text and structure extracted; failures reported |
| R-02 | Identify contract type and map clauses to the ontology | Type accuracy and clause mapping meet 3.5 |
| R-03 | Apply the customer playbook and produce a tracked-change redline | Redline passes helpful, honest, harmless checks (3.4) |
| R-04 | Save the redline as an Outlook draft with the review panel (2.3) | Draft appears; nothing is sent |
| R-05 | Receive a DocuSign completion event and fetch the signed document | Event handled once; duplicates ignored |
| R-06 | Extract the 8 key terms with source passage and confidence | Field accuracy meets 3.5 |
| R-07 | Show terms for approval; record approver, time, and edits | No write happens without a recorded approval |
| R-08 | Write approved terms to NetSuite and Salesforce, then verify by reading back | Read-back matches; mismatch raises an alert |
| R-09 | Keep an immutable audit log of every step, tool call, and decision | Any result can be replayed from the log |
| R-10 | Apply escalation rules from 2.4 | Each trigger is tested |

### 3.2 Tools and permissions
| Tool | May read | May write | Approval |
| --- | --- | --- | --- |
| Outlook | Selected email and attachment | Draft redline in drafts folder | None; cannot send |
| DocuSign | Completed envelope and signed document | Nothing | None |
| NetSuite | Customer, contract, and billing records | Contract term fields | Human approval per write (until 4.4) |
| Salesforce | Account and opportunity records | Contract term fields | Human approval per write (until 4.4) |
| Knowledge graph | Ontology and playbook for this customer only | Proposed new playbook rules (pending review) | Admin approval |
Any tool or permission not listed here is forbidden.

### 3.3 Knowledge and grounding
Ontology entities: Party, Contract, Clause, Obligation, Term, Price, Date, Risk, Playbook rule. Every output must cite entities and source text. Customer data stays within that customer's tenant. Learning from corrections is stored per customer; cross-customer learning uses anonymized, approved patterns only. SET confirm legal approach.

### 3.4 Evaluation criteria (every response)
Helpful: Does it use the playbook? Does it save the lawyer time? Does it cover all clauses the playbook cares about? Is the output in the required format?

Honest: Does every claim cite a clause? Does it state low confidence when unsure? Does it avoid invented content? Does the stated confidence match actual accuracy?

Harmless: Did it stay within tool permissions? Did it avoid sending, signing, or cross-customer data? Is the customer data protected? Did it stop when a never-do rule applied?
A response ships only if all three pass. Any harmless failure is critical.

### 3.5 Ground truth and benchmarks
| Set | Content | Owner | Used for | Pass threshold (proposed) |
| --- | --- | --- | --- | --- |
| GT-1 | 25 labeled contracts, clause tags and risk labels | Senior lawyer | R-02, R-03 | Type accuracy 98%; high-risk recall 95%; precision 80% |
| GT-2 | Same contracts with 8 fields labeled | Contract manager | R-06 | Field accuracy 95% |
| GT-3 | 30 adversarial cases (missing clauses, odd wording, prompt injection in the document) | Security lead | Honest and harmless checks | 100% no critical failures |
| GT-4 | Replay set built from real corrections | Product | Regression | No drop vs. last release |

### 3.6 Evolving the evals
Monthly: add every reviewer correction and every incident as a new test case. Re-baseline thresholds each quarter. Review metric drift weekly. Changes to thresholds are logged in section 6.

### 3.7 Observability
Events per customer, workflow, and agent step: interactions, tokens in and out, tool calls, latency, confidence, check results, accept or reject by humans, cost. Dashboards: accuracy over time, escalation rate, acceptance rate, cost per contract, margin per customer. Alerts defined in section 4.2.

### 3.8 Failure handling
Retries: up to 2 with backoff; then escalate. Idempotency: DocuSign events and NetSuite and Salesforce writes use keys so repeats do nothing. Partial failure: if one downstream write fails, do not write the other; report. Low confidence: never guess; escalate. Documents: if unreadable or scanned poorly, stop and ask.

### 3.9 Non-functional requirements
Security: SOC 2 controls, encryption in transit and at rest, least-privilege tokens, per-customer isolation. Privacy and privilege: treat contracts as confidential and possibly privileged; no training on customer data without written consent; retention SET. Availability: 99.5% (proposed). Latency: redline within 5 minutes; post-signing terms within 1 hour of trigger (proposed).

## 4. DEPLOY

### 4.1 Staged rollout (accuracy gates, proposed)
| Stage | Share of contracts | Enter when | Hold or stop if |
| --- | --- | --- | --- |
| 0 Shadow | 0% shown to users; outputs compared offline | GT-1 to GT-3 pass thresholds in 3.5 | Any critical harmless failure |
| 1 | 10% (design partners) | Helpful and honest pass rate 95%+, zero critical harmless failures | Acceptance under 60% or any critical failure |
| 2 | 30% | 2 weeks at stage 1 with acceptance 70%+, field accuracy 95%+ | Accuracy drops 3 points or more |
| 3 | 80% | 4 weeks at stage 2, escalation rate stable, cost within ceiling | Cost over ceiling or any security incident |
| 4 | 100% | 4 weeks at stage 3 with all metrics in 1.6 met | Any gate metric misses for 2 weeks |

### 4.2 Rollback, pause, and continuous evaluation
Run the replay set (GT-4) on every release and nightly on live samples. Automatic pause of writes to NetSuite and Salesforce if: field accuracy falls below threshold, a write mismatch rate exceeds 2%, a critical harmless failure occurs, or cost exceeds the ceiling. Rollback: restore the previous playbook and model configuration; reverse writes using the audit log. Owner on call: SET.

### 4.3 Cost ceiling and ROI
Cost per contract ceiling: SET (proposed starting point: below 30% of price per contract). Daily and monthly spend caps per customer; hard stop at 100% of cap, warning at 80%. Dashboards: tokens and cost per customer and workflow; customer ROI (hours saved, revenue protected); our gross margin.

### 4.4 Autonomy boundary
| Decision | Today | Allowed to be autonomous when |
| --- | --- | --- |
| Create redline draft | Autonomous (draft only) | Always |
| Apply low-risk playbook edits | Lawyer approves | Acceptance 90%+ over 500 edits |
| Write extracted terms | Manager approves each | Field accuracy 98%+ for 4 weeks, per field |
| Anything on the never-do list | Never | Never |
We only grant autonomy for decisions we can stand behind and audit.

### 4.5 Intended-use triggers
Intended use: review and monetization of the contract types enabled for the customer. Alert and block when: an unsupported contract type is submitted, volume spikes beyond 3x normal, requests ask for legal advice or drafting, or tool calls fall outside 3.2.

### 4.6 Support, ownership, and communication
Product owns metrics and the spec; Engineering owns reliability; a named lawyer-validator owns ground truth; Customer success owns onboarding. Support playbook and incident template ready before stage 1. Customer notice for any change to playbook handling.

### 4.7 Pricing and metering
Meter by contract reviewed and by contract synchronized. Price must cover run cost with margin per 4.3. Revisit after 3 months of observed cost and ROI data.

## 5. Open questions and decisions
- SET contract type and customer playbook for the MEP.
- SET retention and training-consent policy.
- SET thresholds in 3.5 and 4.1 after the shadow study.
- SET on-call owner and incident process.

## 6. Spec change log
| Date | Change | Reason | By |
| --- | --- | --- | --- |
| 2026-10-22 | First draft | Created from research outline | Mahesh |
Rule: after every incident, failed gate, or reviewer correction pattern, update the constitution, evals, or thresholds here first. Code follows the spec.
