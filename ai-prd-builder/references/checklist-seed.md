# Checklist starter (one-time copy)

This file is NOT the checklist. The living checklist is `checklist.md` in the user's own folder (`CHECKLIST_PATH`). Use this file only to create that file when it does not exist, after the user says yes. After that, never read this file as the checklist, because the user's copy may have changed.

The starter rows are the same as `checklist/checklist.md` at the root of the repo this skill ships in: copy that file into the user's folder, and create `checklist-changelog.md` with the first line shown at the end.

Columns: ID, D (Discover, Design, Develop, Deploy, General), checkpoint, how it is tested, status, date added.

| ID | D | Checkpoint |
|----|---|------------|
| C01 | Discover | Gap test: why a general AI tool is not enough |
| C02 | Discover | Why now and why us, with evidence |
| C03 | Discover | Riskiest assumption with a test and a kill threshold |
| C04 | Discover | MEP: smallest version that can be scored |
| C05 | Design | Trust design: plan, knowledge used, iterations, evaluations shown to the user, layered |
| C06 | Design | Confidence and items for the human to validate |
| C07 | Design | Constitution: never-do list, priority order, tone and output format |
| C08 | Design | Escalation rules: when the system stops and asks, and whom |
| C09 | Develop | Helpful, honest, harmless criteria for every response |
| C10 | Develop | Ground truth and benchmarks per use case, with an owner |
| C11 | Develop | Tool permissions: what each tool reads and writes, and approvals |
| C12 | Develop | Observability per customer, workflow and agent: interactions, tokens, accuracy |
| C13 | Deploy | Rollout gated by accuracy, with rollback and continuous evaluation |
| C14 | Deploy | Cost ceiling and ROI dashboards |
| C15 | Deploy | Autonomy boundary and intended-use triggers |
| C16 | Discover | North Star and roadmap steps |
| C17 | Discover | Problem and user evidence |
| C18 | Discover | Success metrics tied to the North Star |
| C19 | Design | Roles, authority and journeys with pause points |
| C20 | Design | Good, bad and borderline output examples |
| C21 | Design | Scope: in, out, later |
| C22 | Develop | Requirements with IDs and a done-when |
| C23 | Develop | Knowledge, ontology and data boundaries |
| C24 | Develop | Evolving evals |
| C25 | Develop | Failure handling |
| C26 | Develop | Security, privacy, privilege, retention, audit log |
| C27 | Deploy | Support, ownership and incident process |
| C28 | Deploy | Pricing and metering |
| C29 | General | Open questions and SET list; starting numbers labeled proposed |
| C30 | General | Spec change log and living-spec rule |
| C31 | General | Header for coding agents: build order, stop-and-ask rule, ID rule |

For each row the user's copy also holds a "how it is tested" column, status (active) and date added. When creating the file, write that column from the checkpoint wording (for example, C03 is tested by: assumption, test and number all present). First line for `checklist-changelog.md`:
2026-10-22 | initial 31 rows | seeded from the PRD research outline | Mahesh Yadav
