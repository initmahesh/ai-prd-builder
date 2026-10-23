# Living PRD checklist for AI products

Edit by hand or approve additions proposed by ai-prd-builder. Never delete a row: set Status to retired and say why in the change log.
Columns: ID, D (Discover, Design, Develop, Deploy, General), checkpoint, how it is tested, status, date added.

| ID | D | Checkpoint | How it is tested | Status | Added |
|----|---|------------|------------------|--------|-------|
| C01 | Discover | Gap test: why a general AI tool is not enough | PRD answers each reason (restrictions, no shared learning, craft planner, data and ontology quality, accountability) with product-specific evidence, or says which do not hold | active | 2026-10-22 |
| C02 | Discover | Why now and why us, with evidence | Both stated; each claim has a source or a SET label | active | 2026-10-22 |
| C03 | Discover | Riskiest assumption with a test and a kill threshold | Assumption, test and number all present | active | 2026-10-22 |
| C04 | Discover | MEP: smallest version that can be scored | Scope, evals and ground truth for the smallest version are named | active | 2026-10-22 |
| C05 | Design | Trust design: plan, knowledge used, iterations, evaluations shown to the user, layered | Each layer named; answer shown first | active | 2026-10-22 |
| C06 | Design | Confidence and items for the human to validate | Confidence labels and a validate list with a fast accept, edit or reject action | active | 2026-10-22 |
| C07 | Design | Constitution: never-do list, priority order, tone and output format | All three present and specific | active | 2026-10-22 |
| C08 | Design | Escalation rules: when the system stops and asks, and whom | Table of triggers, who is asked, behavior while waiting | active | 2026-10-22 |
| C09 | Develop | Helpful, honest, harmless criteria for every response | Questions listed for each of the three; harmless failures marked critical | active | 2026-10-22 |
| C10 | Develop | Ground truth and benchmarks per use case, with an owner | Sets, owner, use and pass thresholds listed | active | 2026-10-22 |
| C11 | Develop | Tool permissions: what each tool reads and writes, and approvals | Table with read, write and approval for every tool; anything unlisted forbidden | active | 2026-10-22 |
| C12 | Develop | Observability per customer, workflow and agent: interactions, tokens, accuracy | Events and dashboards listed | active | 2026-10-22 |
| C13 | Deploy | Rollout gated by accuracy, with rollback and continuous evaluation | Stages with entry numbers; pause and restore triggers | active | 2026-10-22 |
| C14 | Deploy | Cost ceiling and ROI dashboards | Ceiling, caps and what is tracked for ROI and our cost | active | 2026-10-22 |
| C15 | Deploy | Autonomy boundary and intended-use triggers | Table of decisions with when autonomy is allowed; alerts for out-of-purpose use | active | 2026-10-22 |
| C16 | Discover | North Star and roadmap steps | North Star plus ordered steps, each unlocking the next | active | 2026-10-22 |
| C17 | Discover | Problem and user evidence | Who has the pain, with data or interviews or a SET label | active | 2026-10-22 |
| C18 | Discover | Success metrics tied to the North Star | Metrics with numbers marked proposed or confirmed | active | 2026-10-22 |
| C19 | Design | Roles, authority and journeys with pause points | Roles table; journeys show where the system pauses | active | 2026-10-22 |
| C20 | Design | Good, bad and borderline output examples | One of each | active | 2026-10-22 |
| C21 | Design | Scope: in, out, later | Three lists | active | 2026-10-22 |
| C22 | Develop | Requirements with IDs and a done-when | Every requirement has an ID and a testable done-when | active | 2026-10-22 |
| C23 | Develop | Knowledge, ontology and data boundaries | Entities, sources and per-customer isolation stated | active | 2026-10-22 |
| C24 | Develop | Evolving evals | Cadence and how failures become tests | active | 2026-10-22 |
| C25 | Develop | Failure handling | Retries, repeat safety, partial failure, low confidence | active | 2026-10-22 |
| C26 | Develop | Security, privacy, privilege, retention, audit log | Each stated, or SET | active | 2026-10-22 |
| C27 | Deploy | Support, ownership and incident process | Named owners and an incident path | active | 2026-10-22 |
| C28 | Deploy | Pricing and metering | What is metered and how price covers run cost | active | 2026-10-22 |
| C29 | General | Open questions and SET list; starting numbers labeled proposed | List present; no unlabeled starting number | active | 2026-10-22 |
| C30 | General | Spec change log and living-spec rule | Log table and the rule that specs change first | active | 2026-10-22 |
| C31 | General | Header for coding agents: build order, stop-and-ask rule, ID rule | All present at the top | active | 2026-10-22 |
