# Design spec: PRD.md structure

The structure of every PRD this skill writes. Sections follow the four D's. Fill each from the confirmed interview; if something is unknown, show the section with the gap tagged, never blank.

## Required sections (in order)
Header: title, version, owner, status, updated date, and a one-line pointer to the change log.
0. How to use this file: for people (read sections 1 and 2 for why and experience, 3 and 4 for what must be true to build and ship); for coding agents (build only what is in scope, every requirement has an ID, stop and ask when a requirement is ambiguous, conflicts with the constitution or needs an unlisted tool, build order, a requirement is done only when its evals pass).
1. Discover: 1.1 North Star and roadmap; 1.2 Problem and user evidence; 1.3 Why now and why us; 1.4 Gap test; 1.5 Riskiest assumption; 1.6 Success metrics; 1.7 MEP; 1.8 Competitive context (short).
2. Design: 2.1 Users and roles; 2.2 Journeys with pause points; 2.3 Trust design (layered); 2.4 Constitution (never-do, priority order, tone and output format, escalation table); 2.5 Examples (good, bad, borderline); 2.6 Scope (in, out, later).
3. Develop: 3.1 Requirements with IDs and done-when; 3.2 Tools and permissions table; 3.3 Knowledge and grounding; 3.4 Evaluation criteria (helpful, honest, harmless); 3.5 Ground truth and benchmarks; 3.6 Evolving the evals; 3.7 Observability; 3.8 Failure handling; 3.9 Security, privacy, privilege, availability.
4. Deploy: 4.1 Staged rollout; 4.2 Rollback, pause and continuous evaluation; 4.3 Cost ceiling and ROI; 4.4 Autonomy boundary; 4.5 Intended-use triggers; 4.6 Support, ownership, communication; 4.7 Pricing and metering.
5. Open questions and SET list.
6. Spec change log (date, change, reason, by) and the rule: after every incident, failed gate or reviewer correction pattern, update the constitution, evals or thresholds in this file first.

## Style
- Plain business English, short sentences, tables for roles, tools, escalation, rollout and ground truth.
- Every starting number is labeled proposed. Every fact has a link and date, or a SET label.
- Cite the clause or source for each claim in examples.

## Pattern example (a pattern, never content for another product)
Full worked example: `references/example-prd.md`. Before-and-after contrast: `references/baseline-prd.md`.
A contract risk and monetization product: before signing it reads a contract in Outlook, redlines it and saves a draft; after signing a DocuSign event triggers term extraction, which a human approves before it is written to NetSuite and Salesforce. Tools table: Outlook (draft only, cannot send), DocuSign (read only), NetSuite and Salesforce (write after approval).

## Missing data
Show the section with the gap tagged. Never leave a blank box or drop the section.
