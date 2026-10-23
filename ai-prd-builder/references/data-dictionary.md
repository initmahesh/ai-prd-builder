# Data dictionary: ai-prd-builder

The single source of truth for names and definitions. SKILL.md refers to this file and never restates it.

| Source | Object (table, sheet, file) | Field | Definition | Freshness rule |
|--------|-----------------------------|-------|------------|----------------|
| User's folder | checklist.md | Row | One checkpoint: ID, D, checkpoint, how it is tested, status, date added | Read at the start of every run |
| User's folder | checklist.md | Status | active (checked every run) or retired (kept, not checked) | Never deleted |
| User's folder | checklist-changelog.md | Line | Date, change, reason, approver | Appended at CP5 only |
| Web | Page used as evidence | Source entry | URL, date, opened or search-only | Prefer pages from the last 6 months; note the date |

## Term definitions
| Term | Definition | Rule |
|------|------------|------|
| Agent | An AI system with tools that can take actions, not only answer | Define on first use in a PRD |
| Gap test | The case for why a general AI tool is not enough | Five reasons, see interview guide |
| MEP | Minimum evaluable product: the smallest version that can be scored against ground truth | Replaces MVP-only thinking |
| Constitution | Never-do list, priority order, tone and output format, escalation rules | Lives in PRD section 2.4 |
| Ground truth | Labeled cases that define the right answer, with an owner | Section 3.5 |
| Helpful, honest, harmless | The three criteria every response must pass | Section 3.4 |
| Autonomy boundary | What the system may decide alone, and when that grows | Section 4.4 |
| proposed | A starting number the user accepted as a default but has not confirmed | Label in the PRD |
| SET | An item only the user can confirm or evidence only the user can supply | Listed in section 5 of the PRD |
