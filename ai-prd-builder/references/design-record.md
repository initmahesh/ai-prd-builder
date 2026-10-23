# Design record: ai-prd-builder

Why the skill is built the way it is.

## The brief (summary)
Interview a user section by section on an AI product PRD (or audit and upgrade an existing PRD), research with cited sources, write PRD.md, and check it against a living checklist kept outside the skill. Output: PRD.md plus a pass/fail report. Run by Mahesh, his students and several teams. Owner: Mahesh Yadav. Built from the research outline "Learn to Build PRDs for Humans and AI Agents" (Appendices B and C).

## Decisions and reasons
| Decision | Reason | Decided by |
|----------|--------|------------|
| Single agent, medium size | Sequential work that fits one context; shared across teams so reference files are needed | Mahesh, CP3 2026-10-22 |
| Checklist lives outside the skill in the user's folder | The checklist must evolve without changing the skill; each team can keep its own | Mahesh, CP1 2026-10-22 |
| Checklist starter copy shipped as references/checklist-seed.md | The skill cannot run without a checklist, so it can create the first copy once | Assumed in design, approved at CP3 |
| Interview one section at a time with proposed defaults | Matches how the PRD was built in the research doc | Mahesh, round 1 |
| Web research with cited sources, on by default | Evidence for why now and the gap test | Mahesh, round 2 |
| Skill proposes checklist changes, user approves | Prevents bad rows from accumulating | Mahesh, round 2 |
| Unknown numbers become labeled defaults plus a SET list | Keeps momentum without inventing facts | Mahesh, round 2 |
| All QA rows are Flag; after 2 attempts deliver marked "checklist not passed" | The user chose flag-only | Mahesh, rounds 2 and 3 |

## Assumptions the user accepted
- Trigger phrases listed in section 2.
- Output file names PRD-product-slug.md and PRD-product-slug-checklist-report.md, saved beside checklist.md.
- Seed checklist of 31 rows (15 core plus 16 extras).
- Default feedback settings: one question per run, update offered after 3 items, snooze 5 runs.
- Memory is off until the owner names a shared folder.

## Admin-dependent practices and the skill-level equivalents used
| Practice | Equivalent |
|----------|------------|
| Rate limits and spend caps | Soft caps in config: searches, rounds, QA attempts, rebuilds |
| Connectors | Web search and a user-connected folder only; fallbacks in config |
| Scheduling | Not applicable; always started by the user |
| Model tier | Session model |

## Known limits
- The skill cannot run without access to a folder holding checklist.md (or a yes to create one).
- With "flag everything", a PRD with missing checklist rows is still delivered, marked "checklist not passed".
- The seed checklist reflects one author's research; teams should adapt it.
