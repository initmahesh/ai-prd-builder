# QA checklist: ai-prd-builder

Checks of the finished PRD and report. One row per check; a different person could run each and reach the same answer. Every row is a Flag in this skill: nothing blocks delivery. Flag rows are listed first in the report.

| ID | Check | How to verify | Source of truth | Tier |
|----|-------|---------------|-----------------|------|
| Q1 | Every active row in checklist.md has a row in the report with pass, partial or missing and a section reference | Count active rows in the file and report rows | checklist.md at CHECKLIST_PATH | Flag |
| Q2 | Every active checklist row passes in the PRD | Read the PRD against each row's test | checklist.md | Flag |
| Q3 | Every fact, number or quote has a source link and date, a proposed label, or a SET label | Scan the PRD; flag any bare claim | SKILL.md section 8 | Flag |
| Q4 | Every tool lists what it reads, what it writes and its approval | Read the tools table | design-spec.md section 3.2 | Flag |
| Q5 | Wording is specific: no "fast", "accurate" or "secure" without a number or condition | Scan for vague words | SKILL.md section 8 | Flag |
| Q6 | Terms such as agent, ground truth and ontology are defined once | Check first use | data-dictionary.md | Flag |
| Q7 | Numbers agree across sections (targets, thresholds, stages) | Compare metrics, evals and rollout | The PRD | Flag |
| Q8 | All required sections exist, and gaps are tagged, not blank | Compare with the section list | design-spec.md | Flag |
| Q9 | A SET list exists and every proposed number is labeled | Search for the labels | SKILL.md section 8 | Flag |
| Q10 | No confidential or personal data from the user's input is in memory, the run log or the feedback log | Scan those files | SKILL.md section 10 | Flag |

## QA report format

Overall result and attempts used; one line per row (ID, result, evidence); unresolved flags; source dates; then the checklist table (ID, result, where covered, what to add).
