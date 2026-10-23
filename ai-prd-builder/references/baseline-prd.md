# Baseline PRD (traditional, before the checklist): Contract Risk and Monetization Platform

A traditional 2-page PRD for the contract product. It fails all 31 checklist rows' spirit, in particular the 15 core ones. Use it in existing-PRD mode as an example of what the audit finds. Numbers and dates are placeholders.

**Owner:** Product  |  **Status:** Draft

## 1. Overview and problem
Legal teams spend hours reviewing and redlining contracts by hand, and after signing, key commercial terms are rarely entered into billing and sales systems, so revenue is missed or delayed. This product reviews contracts before signing, and moves the key terms of signed contracts into downstream systems.

## 2. Goals and success metrics
- Cut average first-pass contract review time by 50%.
- Capture key commercial terms for 95% of signed contracts within 24 hours of signing.
- Reduce billing errors caused by missed terms by 30%.
- Why now: contract volume is growing and teams want to automate manual work.

## 3. Users
In-house legal counsel, contract managers, finance and billing operations, sales operations.

## 4. Market and competition
Contract lifecycle tools already exist (CLM suites, e-signature platforms). Our differentiator is combined pre-signing review and post-signing monetization.

## 5. User stories and acceptance criteria
| Story | Acceptance criteria |
| --- | --- |
| As a lawyer, I want to open a contract from Outlook and get a redlined draft back so I can save review time | Redlined draft appears in Outlook drafts within 5 minutes; changes are tracked |
| As a contract manager, I want key terms extracted after DocuSign completes so billing is set up on time | Terms (price, term, renewal, escalators) extracted within 24 hours of signing |
| As a finance user, I want terms to appear in NetSuite and Salesforce so I do not re-key them | Records created or updated in both systems with no manual entry |

## 6. Scope
- In: Outlook integration, redlining, DocuSign trigger, term extraction, NetSuite and Salesforce updates.
- Out: contract drafting from scratch, other e-signature tools, other ERPs and CRMs.
- Later: more contract types, reporting dashboard.

## 7. User experience
Lawyer flow: receive contract email, click Review, receive redlined draft. Finance flow: signed contract triggers extraction; terms appear in NetSuite and Salesforce. Wireframes are in the design file.

## 8. Requirements
- Functional: read attachments, redline, create Outlook drafts, receive DocuSign events, extract terms, write to NetSuite and Salesforce.
- Non-functional: SOC 2 controls, encryption in transit and at rest, 99.5% availability, response within 5 minutes.
- Dependencies: Outlook, DocuSign, NetSuite and Salesforce APIs and customer admin approvals.

## 9. Timeline and stakeholders
- Design complete: Nov 2026. Build complete: Jan 2027. Beta: Feb 2027. General availability: Apr 2027.
- Stakeholders (RACI): Product (accountable), Engineering (responsible), Legal and Finance (consulted), Sales operations (informed).

## 10. Launch and risks
- Launch: beta with three customers behind a feature flag, then general availability. Support trained before launch.
- Risks: integration delays, customer security reviews. Mitigation: early API access, security documentation.
